---
title: Hide annoying terminal window for .NET Core GUI Apps
---

Hide annoying terminal window for .NET Core GUI Apps
===

When one wants to build a .NET Core Cross Platform UI App, there is always the annoying Terminal window displayed.

That happens when you dont compile from Windows and/or Visual Studio and the wrong binary type is set.

Luckily there exists a nuget package which solves this:

```sh
dotnet add package NSubsys --version 1.0.0
```

> An alternative to this would be using editbin.exe, which only comes with Visual Studio, so thats not an option for me.

In addition add this to your csproj as NSubsys does not work well with dotnet build itself:

```xml
<PropertyGroup>
    <NSubsysTasksPath Condition="'$(NSubsysTasksPath)' == ''">$(NugetPackageRoot)/nsubsys/1.0.0/tool/NSubsys.Tasks.dll</NSubsysTasksPath>
</PropertyGroup>

<UsingTask TaskName="NSubsys.Tasks.NSubsys" AssemblyFile="$(NSubsysTasksPath)" />

<Target Name="CustomAfterBuild" AfterTargets="Build" Condition="$(RuntimeIdentifier.StartsWith('win'))">
   <NSubsys TargetFile="$(OutputPath)$(AssemblyName)$(_NativeExecutableExtension)" />
</Target>

<Target Name="CustomAfterPublish" AfterTargets="Publish" Condition="$(RuntimeIdentifier.StartsWith('win'))">
    <NSubsys TargetFile="$(PublishDir)$(AssemblyName)$(_NativeExecutableExtension)" />
</Target>
```
