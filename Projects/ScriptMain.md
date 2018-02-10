# Script [Main] Section

The main section that defines all the details of your script. This data affects how your script is displayed in PEBakery's user interface as well as how it is processed during a build.

This documentation refers to the `Main` section located within the `.script` files. For documentation relating to the `Main` section for `script.project` refer to `Project Main`.

## Syntax

Script data is stored in .INI style `Key=Value` format.

## Values

The following values are used by PEBakery to define a script and it's behavior. Script developers may define additional values under the `[Main]` section for other uses. These values will be ignored by PEBakery.

| Name | Description |
| --- | --- |
| Title | The title of your script. |
| Description | **(Optional)** A short description of the scripts intended purpose. |
| Author | **(Optional)** The author of the script. |
| Credits | **(Optional)** Acknowledgment of people or teams that contributed to the script's development. |
| Date | **(Optional)** Date the script was released. (Recommended format is YYYY-MM-DD.) |
| Version | **(Optional)** Version number of the script. |
| [Level](./ScriptLevel.md) | Defines the sequence in which the script is processed. **Default** is `0`.|
| Selected | **(Optional)** Defines how the script can be selected for processing. **Default** is `True`. |
|| True - The script is selected in the project tree and will be processed. |
|| False - The script is deselected in the project tree and will not be processed. |
|| None - The script is not allowed to be selected/deselected and will not be processed. Used primarily for configuration and utility scripts. |
| Interface | **(Optional)** Specifies the section that contains the currently displayed Graphical User Interface of the script. Default is `Interface`. |
| Mandatory | **(Optional)** The script will be processed and cannot be disabled. **Default** is `False`.|

## Remarks

None.

## Related

[Project Main](./ProjectMain.md), [Project Process](./ProjectProcess.md), [Project Variables](./ProjectVariables.md), [Script Interface](./ScriptInterface.md), [Script Process](./ScriptProcess), [Script Variables](./ScriptVariables.md), [Script Levels](./ScriptLevels.md)

## Examples

### Example 1

A typical `Main` section for an application script.

```pebakery
[Main]
Title=My App Script
Description=Adds myApp the the project.
Author=Homes32
Credits=Thanks to ied206 for creating PEBakery!
Selected=True
Level=5
Version=1
Date=2018-02-08
```