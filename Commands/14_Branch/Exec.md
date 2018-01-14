# Exec

Runs the commands found in a named `[Section]` of a plugin file.

You can run sections from any plugin including the plugin from which `Exec` was originally called. All variables from the specified plugin's `[variables]` section will be added to the scope of the current plugin. If duplicate variable names exist then the variables in the currently running plugin will be overwritten.

## Syntax

```pebakery
Run,<FileName>,<Section>[,Parameters]
```

### Arguments

| Argument | Description |
| --- | --- |
| FileName | The full path of the plugin. Hint: Use %PluginFile% to reference the current plugin. |
| Section | The name of the section containing the commands you wish to run. |
| Parameters | **(Optional)** Parameters to pass to the `Section` being executed. |

### Tokens

The following tokens can be used to perform additional operations when executing a section.

| Token | Description |
| --- | --- |
| #1, #2, #3, etc. | Used within a `Section` to access any parameters passed. The numbering scheme starts from `1` and continues in the order the parameters were passed. These tokens are discarded when the section is finished processing. |
| #a | Contains the number of parameters passed to `Section`. |
| #r | Return a value from the `Section`. The `#r` token is not affected by the constraints of `System,SetLocal` and can be used to return the value of an isolated variable to the main process. #r is volatile so if you need to preserve the return value copy it into a local variable. |

## Remarks

PEBakery allows an unlimited number of parameters to be passed to the `[section]` being executed. This allows us to create dynamic "functions" containing commands that need to be called repeatedly with different arguments, or used to create a `Macro`.

Although the parameters themselves are passed by value using tokens, all variables are in the scope of the entire plugin, so the original values can modified by referencing them by name. If required, you can use the `System,SetLocal` command to isolate variables modified within the running section.

## Related

[Run](./Run.md), [SetMacro](../15_Control/SetMacro.md), [System,SetLocal](../12_System/SetLocal.md), [System,EndLocal](../12_System/EndLocal.md)

## Examples

### Example 1

In this example we will use the `Exec` to run a command in another plugin.

#### Plugin #1 (Plugin1.script)

```pebakery
[Main]
Title=Exec Example Plugin #1
Description=Show usage of the Exec Command with a parameter.
Level=5
Version=1
Author=Homes32

[variables]
%file%=C:\Temp\myFile.txt

[process]

If,Not,ExistFile,%file%,Begin
  FileCreateBlank,%file%
  TXTAddLine,%file%,"Hello World!",Append
End

// using Run the value of %file% will be taken from this plugin (C:\Temp\myFile.txt)
Run,%ProjectDir%\Plugin2.script,Open-File

// using Exec the value of %file% will be overwritten with the value taken from Plugin2 (C:\Temp\myFile2.txt)
Exec,%ProjectDir%\Plugin2.script,Open-File
```

#### Plugin #2 (Plugin2.script)

```pebakery
[Main]
Title=Exec Example Plugin #2
Description=Show usage of the Exec Command with a parameter.
Level=5
Version=1
Author=Homes32

[variables]
%file%=C:\Temp\myFile2.txt

[process]

[Open-File]
Message,"Opening file: %file%"
ShellExecute,Open,notepad.exe,%file%
```