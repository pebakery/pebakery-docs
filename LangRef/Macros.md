# Macros

Macros are defined as procedures to be executed when a specific keyword is encountered.

Macros make script maintenance easier as the code is written only once but can be called repeatedly by any number of scripts or processes. They are ideal for repetitive tasks such as creating shortcuts or downloading and unpacking a file.

## Defining a Macro

Macros can be defined several different ways.

1. The [Variables] section of a _.script_ or _script.project_ file.
1. The SetMacro command.
1. The projects Application Programming Interface (API) definition.

Macro names can only consist of following characters `a-z A-Z 0-9 _ ( )`. Because macros are parsed before run-time using %Variables% in the macro name is not supported.

### Defining a Macro with the [Variables] Section

Macros are defined using the .INI style `Key=Value` format. Unlike variables the macro name is **not** enclosed in `%` signs.

```pebakery
[Variables]
myMacro=Run,%PluginFile%,DoSomething
```

For more details see [Script Variables](/Projects/ScriptVariables.md) and [Project Variables](/Projects/ProjectVariables.md).

### Defining a Macro with the `SetMacro` command

See the documentation for the [SetMacro](/Commands/Control/SetMacro.md) command.

### Defining a "Macro Library"

The following variables may be used within the _script.project_ Variables section to define a custom "Macro Library" that will be available to the entire project.

| Variable | Description |
| --- | --- |
| %API% | The full path to a script file containing a "Macro Library". |
| %APIVAR% | The name of the section within the script defined by `%API%` that contains the Macro Definitions to be loaded into the GLOBAL project scope. |

For more details see [Project Variables](/Projects/ProjectVariables.md).