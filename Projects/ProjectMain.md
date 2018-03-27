# Project [Main] Section

The main section that defines all the details of your project.

This documentation refers to the `Main` section located within the `script.project` file. For documentation relating to the `Main` section of individual scripts refer to `Script Main`.

## Syntax

Project data is stored in .INI style `Key=Value` format.

## Values

The following values are used by PEBakery to define a project. Project developers may define additional values under the `[Main]` section for other uses. These values will be ignored by PEBakery.

| Name | Description |
| --- | --- |
| Title | The title of your project. |
| Description | **(Optional)** A short description of the project. |
| Author | **(Optional)** The author of the project. |
| Credits | **(Optional)** Acknowledgment of people or teams that contributed to the project's development. |
| Date | **(Optional)** Date the project was released. (Recommended format is YYYY-MM-DD.) |
| Version | **(Optional)** Version number of the project. |
| Interface | **(Optional)** Specifies the section that contains the currently displayed Graphical User Interface. Default value is `Interface`. |
| PathSetting | `True`/`False` - Enable modifying `SourceDir`, `TargetDir`, and `IsoFile` from PEBakery's Settings dialog. |
| SourceDir | **(Legacy)** Full path to the Windows source files used to build the project. If `PathSetting=True` the value is copied to `GLOBAL` variable `%SourceDir%` at build time. |
| TargetDir | **(Legacy)** Full path to the directory where the project will be built. If `PathSetting=True` the value is copied to `GLOBAL` variable `%TargetDir%` at build time. |
| IsoFile | **(Legacy)** Full path to the .iso file to be generated. If `PathSetting=True` the value is copied to `GLOBAL` variable `%IsoFile%` at build time. |

`SourceDir`, `TargetDir`, and `IsoFile` are included for compatibility with Winbuilder 082. They are not required for PEBakery projects, which generally store their paths in a GLOBAL variable.

## Remarks

None.

## Related

[Project Process](./ProjectProcess.md), [Project Variables](./ProjectVariables.md), [Script Interface](./ScriptInterface.md), [Script Main](./ScriptMain.md), [Script Process](./ScriptProcess), [Script Variables](./ScriptVariables.md)

## Examples

### Example 1

A typical project `Main` section.

```pebakery
[Main]
Title=MyWinPE
Description=My PEBakery project
Author=James Bond
Version=1
Date=2018.02.10
PathSetting=False
```

### Example 2

A typical "legacy project" `Main` section.

```pebakery
[Main]
Title=Win7PE SE
Description=Win7PE_SE project that supports Win7 DVD x86 and x64
Author=NightMan, YahooUK, JFX, ChrisR
Version=15
Date=2011.02.10
SourceDir=D:\Images\Win7
TargetDir=%baseDir%\Target\Win7PE_SE
ISOfile=%baseDir%\ISO\Win7Pe.iso
```