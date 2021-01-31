# Script [UpdateScript] Section

This sections controls how PEBakery will perform script updates.

## Syntax

Script update data is stored in .INI style `Key=Value` format.

## Values

The following values are used by PEBakery to perform a script update.

| Name | Description |
| --- | --- |
| UpdateType | The update channel used by this script: |
|| Standalone - The script provides it's own update information, independent of the project. This channel is used for 3rd party/independent developers that want to provide script updates independent of the project. |
|| Project - The project author defines the update information for the script. |
| Url | The URL from which the .script will be downloaded. |

## Remarks

None.

## Related

[UpdateProject Section](./ProjectUpdateProject.md), [Project Update](../Usage/ProjectUpdate.md), [Script Update](../Usage/ScriptUpdate.md)

## Examples

### Example 1

```pebakery
[Main]
Title=My App Script
Description=Adds myApp the the project.
Author=Homes32
Credits=Thanks to ied206 for creating PEBakery!
Selected=True
Level=5
Version=1

[UpdateScript]
UpdateType=Standalone
Url=https://myproject.org/pebakery/myScript.script

[Variables]

[Process]
Message,"Hello World!"
```