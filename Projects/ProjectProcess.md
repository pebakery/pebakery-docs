# Project [Process] Section

This sections contains commands that will be executed every time a script in the project is processed.

Commands placed in this section will be executed during a project build or when the `Run` button on the Graphical User Interface is pressed.

This documentation refers to the `Process` section located within the `script.project` file. For documentation relating to the `Process` section of individual scripts refer to `Script Process`.

## Remarks

Because this section is processed **every time** a script in the project is executed, usage of this section should be limited to functions that are Global in nature and are essential to the project. Failure to do so may result in performance penalties and slower build times.

## Related

[Project Main](./ProjectMain.md), [Project Variables](./ProjectVariables.md), [Script Interface](./ScriptInterface.md), [Script Main](./ScriptMain.md), [Script Process](./ScriptProcess), [Script Variables](./ScriptVariables.md)

## Examples

In this example we use the _script.project_ process section to define a cleanup function using `System,ONBUILDEXIT`, to ensure any hives or mounted WIM images are cleaned up, even if a script fails and the build halts.

### Example 1

```pebakery
[Main]
Title=myProject
Description=Example Project
Author=Homes32
Version=1

[Variables]

[Process]
System,ONBUILDEXIT,Exec,%ProjectDir%\script.project,myProject-ONBUILDEXIT

[myProject-ONBUILDEXIT]
// Make sure all registry hives are unloaded.
RegHiveUnload,%RegSystem%
RegHiveUnload,Tmp_Software
RegHiveUnload,%RegDefault%
RegHiveUnload,%RegComponents%
```