---
title: Self contained dotnet binary with all native libs
---

Self contained dotnet binary with all native libs
===

To create a reasonable sized, self contained binary with all the stuff included into ONE binary, turns out you need a hell of property groups.

So after dropping in these:
```xml
<PropertyGroup>
    <!-- ... -->
    <OutputType>WinExe</OutputType>
    <Nullable>enable</Nullable>
    <BuiltInComInteropSupport>true</BuiltInComInteropSupport>
    <ApplicationManifest>app.manifest</ApplicationManifest>
    <AvaloniaUseCompiledBindingsByDefault>true</AvaloniaUseCompiledBindingsByDefault>
    <SelfContained>true</SelfContained>
    <PublishSingleFile>true</PublishSingleFile>
    <IncludeNativeLibrariesForSelfExtract>true</IncludeNativeLibrariesForSelfExtract>
    <PublishTrimmed>true</PublishTrimmed>
    <PublishReadyToRun>true</PublishReadyToRun>
    <DebugType>embedded</DebugType>
    <EnableCompressionInSingleFile>true</EnableCompressionInSingleFile>
    <IncludeAllContentForSelfExtract>true</IncludeAllContentForSelfExtract>
</PropertyGroup>
```

You can run:

```sh
dotnet publish -r <rid>
```

This will bundle all files, including debug symbols, dylib/dlls and what not into one static binary, utilizing trim and and ready2Run.
