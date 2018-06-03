# Script [Process] Section

This sections contains the main logic of the script.

Commands placed in this section will be executed during a project build or when the `Run` button on the scripts Graphical User Interface is pressed.

This documentation refers to the `Process` section located within the `.script` files. For documentation relating to the `Process` section for `script.project` refer to `Project Process`.

## Remarks

None.

## Related

[Project Main](./ProjectMain.md), [Project Process](./ProjectProcess.md), [Project Variables](./ProjectVariables.md), [Script Interface](./ScriptInterface.md), [Script Main](./ScriptMain.md), [Script Variables](./ScriptVariables.md)

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

[Variables]

[Process]
Message,"Hello World!"
```