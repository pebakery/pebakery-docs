# Project [Variables] Section

This section contains GLOBAL variables and macros the scripts in the project need to reference. The variables are loaded into memory when a build is started or a script is run manually and are available to all scripts in the project.

This documentation refers to the `Variables` section located within the `script.project` file. For documentation relating to the `Variables` section of individual scripts refer to `Script Variables`.

## Syntax

Global variables and macros are defined using the .INI style `Key=Value` format. Variables must be enclosed in `%` percent signs.

### Variables

```pebakery
%myGlobalVar%="C:\Temp"
```

### API Variables

The following variables may be used within the _script.project_ Variables section to define a custom "Macro Library" that will be available to the entire project.

| Variable | Description |
| --- | --- |
| %API% | The full path to a script file containing a "Macro Library". |
| %APIVAR% | The name of the section within the script defined by `%API%` that contains the Macro Definitions to be loaded into the GLOBAL project scope. |

### Macros

```pebakery
myMacro=Run,%PluginFile%,DoSomething
```

## Remarks

Note: With Winbuilder it was necessary to load a "Macro Library" by placing the `AddVariables,%API%,ApiVar,GLOBAL` command in the process section of _script.project_. In PEBakery this is not required. Macros defined in the `%API` `APIVAR` section will automatically be loaded in to the GLOBAL scope.

## Related

[Project Main](./ProjectMain.md), [Project Process](./ProjectProcess.md), [Script Interface](./ScriptInterface.md), [Script Main](./ScriptMain.md), [Script Process](./ScriptProcess), [Script Variables](./ScriptVariables.md)

## Examples

### Example 1

```pebakery
[Main]
Title=myProject
Description=Example Project
Author=Homes32
Version=1

[Variables]
%RegSystem%=%TargetDir%\Windows\System32\config\System
%RegSoftware%=%TargetDir%\Windows\System32\config\Software
%RegDefault%=%TargetDir%\Windows\System32\config\Default
%RegComponents%=%TargetDir%\Windows\System32\config\Components
%AutoRunFile%=%TargetDir%\Windows\System32\autorun.cfg
%BootSRC%=D:\PEBakery\Mount\Win10PESE\Source\BootWimSrc
%InstallSRC%=D:\PEBakery\Mount\Win10PESE\Source\InstallWimSrc
%Source_Win%=D:\PEBakery\Mount\Win10PESE\Source\InstallWimSrc\Windows
%Target_Win%=%TargetDir%\Windows
%Source_Sys%=D:\PEBakery\Mount\Win10PESE\Source\InstallWimSrc\Windows\System32
```

### Example 2

In this example we define a .script file called _myMacroLibrary.script_ as our projects "API" script and load all macros into the Global scope of the project.

```pebakery
[Main]
Title=myProject
Description=Example Project
Author=Homes32
Version=1

[Variables]
%API%=%ProjectDir%\Build\myMacroLibrary.script
%APIVAR%=MacroDef

```