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
| SourceDir | Full path to the Windows source files used to build the project. The value is copied to `GLOBAL` variable `%SourceDir%` at build time. |
| TargetDir | Full path to the directory where the project will be built. The value is copied to `GLOBAL` variable `%TargetDir%` at build time. |
| IsoFile | Full path to the .iso file to be generated. The value is copied to `GLOBAL` variable `%IsoFile%` at build time. |

## Remarks

None.

## Related

[Project Process](./ProjectProcess.md), [Project Variables](./ProjectVariables.md), [Script Interface](./ScriptInterface.md), [Script Main](./ScriptMain.md), [Script Process](./ScriptProcess), [Script Variables](./ScriptVariables.md)

## Examples

### Example 1

A typical `Main` section for an project.

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