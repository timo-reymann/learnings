---
title: Work/.NET/Make dotnet-sonar-scanner evaluate non .NET files
---
 Make dotnet-sonar-scanner evaluate non .NET files
===

dotnet-sonar-scanner can also execute analysis on other files in the projects, e.g. frontend code or tooling, pipeline code.

The setup is a bit tricky and requires a dummy project:

e.g. the following `sonar.csproj`
```xml
<!-- [hv_1.1|Classification: CONFIDENTIAL, DeepL SE] -->
<Project ToolsVersion="14.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <!-- The only purpose of this project is to specify additional files to be analyzed by the SonarScanner for MSBuild -->
  <PropertyGroup>
    <ProjectGuid>{2C84551C-19DC-4865-B9EE-70EC908BDD08}</ProjectGuid>
  </PropertyGroup>

  <!-- 2. Specify the files to be analysed -->
  <ItemGroup>
    <!-- TODO Add file paths to execute analysis for -->
    <SonarQubeAnalysisFiles Include="python/**/*.py" />
  </ItemGroup>


  <!-- ******************************************************** -->
  <!-- Boilerplate - no need to change anything below this line -->
  <!-- ******************************************************** -->
  <!-- Import the SQ targets (will only exist if the scanner "begin" step has been executed) -->
  <PropertyGroup>
    <SQImportBeforeTargets>$(localappdata)\Microsoft\MSBuild\$(MSBuildToolsVersion)\Microsoft.Common.targets\ImportBefore\SonarQube.Integration.ImportBefore.targets</SQImportBeforeTargets>
  </PropertyGroup>
  <Import Condition="Exists('$(SQImportBeforeTargets)')" Project="$(SQImportBeforeTargets)" />

  <!-- Re-define the standard step of targets used in builds -->
  <Target Name="Build" />
  <Target Name="Clean" />
  <Target Name="VSTest" /> <!-- Especially important when using VSTest Runner -->
  <Target Name="CoreCompile" />
  <Target Name="Rebuild" DependsOnTargets="Clean;Build" />

  <!-- Re-define one of the standard SQ targets as we have already set the list of files to analyze above -->
  <Target Name="CalculateSonarQubeFilesToAnalyze" >
    <PropertyGroup>
      <!-- Set a property indicating whether there are any files to analyze -->
      <AnalysisFilesExist Condition=" @(SonarQubeAnalysisFiles) != '' ">true</AnalysisFilesExist>
    </PropertyGroup>
  </Target>
</Project>
```

