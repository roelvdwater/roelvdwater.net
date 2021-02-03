---
layout: post
title: "Understanding the target dependency differences between Cake and NUKE"
date: 2021-02-03 08:00:00 +0100
tags: [Build automation, Cake, NUKE, C#]
author: "Roel van de Water"
---

In the past couple of years I've worked quite a bit with [Cake](https://cakebuild.net), but since about a year I started working with [NUKE](https://nuke.build/). Apart from the differences in syntax, most things are pretty similar in both systems. However, there was one thing which I didn't realize and eventually cost me some time to understand why something wasn't working as intended. Obviously I would have known this if I would have read the NUKE's [fundamentals documentation](https://nuke.build/docs/authoring-builds/fundamentals.html) upfront thoroughly.

## IsDependentOn() and DependsOn()

You might know that in Cake you can use the `IsDependentOn()` method to define a dependency on another target in your target definition. In NUKE, you have a similar method, `DependsOn()`, which also allows you to specify a dependency on another target. Here's the catch: in NUKE the dependency is solely specified at individual targets. Let's take a look at the following NUKE build class:

```csharp
class Build : NukeBuild
{
    public static int Main() => Execute<Build>(x => x.Compile);

    Target Compile => _ => _
        .Executes(() => { });

    Target Deploy => _ => _
        .DependsOn(Compile)
        .Executes(() => { });

    Target InstallService => _ => _
        .DependsOn(Deploy)
        .Executes(() => { });

    Target StartService => _ => _
        .Executes(() => { });

    Target FullDeploy => _ => _
        .DependsOn(InstallService, StartService);
}
```

When I ran the `FullDeploy` target, I expected the execution order to be `Compile`, `Deploy`, `InstallService`, `StartService`. The output shows you this is not the case:

```
═══════════════════════════════════════
Target             Status      Duration
───────────────────────────────────────
StartService       Executed      < 1sec
Compile            Executed      < 1sec
Deploy             Executed      < 1sec
InstallService     Executed      < 1sec
───────────────────────────────────────
Total                            < 1sec
═══════════════════════════════════════
```

Since the dependencies are only specified at individual targets, this does not guarantee that `InstallService` and its dependencies will run before `StartService`. It specifies that `FullDeploy` has a dependency on both `InstallService` and `StartService`, but it doesn't mean that the given parameter sequence matches the execution order, including their dependencies.

## Before() and After()

If you want dependencies to run in a certain order, you can use the `Before()` and `After()` methods on your targets. For instance, in the above example, we want the `StartService` target to run after `InstallService` when it runs in conjunction with other targets in the `FullDeploy` target. This can be achieved in two ways:

```csharp
Target InstallService => _ => _
    .DependsOn(Deploy)
    .Before(StartService)
    .Executes(() => { });
```

or

```csharp
Target StartService => _ => _
    .After(InstallService)
    .Executes(() => { });
```

The first example makes sure that when `InstallService` runs together with `StartService`, `InstallService` executes **before** `StartService`. The second example has the same result but defines it the other way around: when `StartService` runs together with `InstallService`, `StartService` executes **after** `InstallService`.

## Summary

If you're using `DependsOn()` in NUKE and also have targets that depend on other targets, make sure to check if you need to specify in which order targets need to run by using `Before()` or `After()`. This subtle but important difference between Cake and NUKE can lead to unexpected behavior which can be hard to debug.
