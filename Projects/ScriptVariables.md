# Script [Variables] Section

This section contains any predefined variables and macros the script needs to reference. The variables are loaded into memory when the script is processed during a build, a section within the script is called using the `Exec` command, or when another script loads them with the `AddVariables` command.

This documentation refers to the `Variables` section located within the `.script` files. For documentation relating to the `Variables` section for `script.project` refer to `Project Variables`.

## Syntax

Script variables and macros are defined using the .INI style `Key=Value` format. Variables must be enclosed in `%` percent signs.

### Variables

```pebakery
%myProgramName%="My Program"
```

### Macros

```pebakery
myMacro=Run,%PluginFile%,DoSomething
```

Note that the macro name is **not** enclosed in `%` signs.

## Remarks

None.

## Related

[AddVariables](/Commands/Control/AddVariables.md), [Exec](/Commands/Branch/Exec.md), [Project Main](./ProjectMain.md), [Project Process](./ProjectProcess.md), [Project Variables](./ProjectVariables.md), [Script Interface](./ScriptInterface.md), [Script Main](./ScriptMain.md), [Script Process](./ScriptProcess), [Macros](/LangRef/Macros.md)

## Examples

### Example 1

```pebakery
[Main]
Title=Variables Section
Description=Variables Section Example
Author=Homes32
Level=5
Version=1

[Variables]
%myProgramName%="My Program"
myMacro=Run,%ScriptFile%,EchoMessage

[Process]
myMacro,%myProgramName%

[EchoMessage]
Echo,#1
Message,#1
```