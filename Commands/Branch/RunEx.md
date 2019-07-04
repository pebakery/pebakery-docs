# RunEx

`RunEx` is an extended form of the standard `Run` command that allows passing parameters by reference as well as by value.

You can run sections from any script including the script from where `RunEx` is originally called but only variables in the scope of the current script will be visible to the section being run.

## Syntax

```pebakery
RunEx,<FileName>,<Section>[,Parameters]
```

### Arguments

| Argument | Description |
| --- | --- |
| FileName | The full path of the script. Hint: Use %ScriptFile% to reference the current script. |
| Section | The name of the section containing the commands you wish to run. |
| Parameters | **(Optional)** Parameters to pass to the `Section` being executed. Parameters must be defined as either `In=` or `Out=`. |
|| In=<%variable%> - Pass by value. |
|| Out=<%variable%> - Pass by reference. If the variable does not exist it will be created. | 

### Tokens

The following tokens can be used to perform additional operations when executing a section.

| Token | Description |
| --- | --- |
| #1, #2, #3, etc. | Used within a `Section` to access `In=` parameters passed. The numbering scheme starts from `1` and continues in the order the `In=` parameters were passed. These tokens are discarded when the section is finished processing. |
| #a | Contains the number of parameters passed to `Section`. |
| #o_n_ | References an `Out=` variable inside the called section. The numbering scheme starts from `1` and continues in the order the `Out=` parameters were passed. These tokens are discarded when the section is finished processing. |
| #r | Return a value from the `Section`. The `#r` token is not affected by the constraints of `System,SetLocal` and can be used to return the value of an isolated variable to the main process. #r is volatile so if you need to preserve the return value copy it into a local variable. |

## Remarks

PEBakery allows an unlimited number of parameters to be passed to the `[section]` being executed. This allows us to create dynamic "functions" containing commands that need to be called repeatedly with different arguments, or used to create a `Macro`.

Although the parameters themselves are passed by value using tokens, all variables are in the scope of the entire script, so the original values can modified by referencing them by name. If required, you can use the `System,SetLocal` command to isolate variables inside the running section.

## Related

[GetParam](/Commands/Control/GetParam.md), [Exec](./Exec.md), [Run](./Run.md), [SetMacro](/Commands/Control/SetMacro.md), [System,SetLocal](/Commands/System/SetLocal.md), [System,EndLocal](/Commands/System/EndLocal.md)

## Examples

### Example 1

In this example we will use the `RunEx` command to execute a section called _Open_File_ and return the operations exit code into the variable we specify.

```pebakery
[Main]
Title=RunEx Example 1
Description=Show usage of the RunEx Command
Level=5
Version=1
Author=Homes32

[Variables]
%file%=C:\Temp\myFile.txt

[process]

If,Not,ExistFile,%file%,Begin
  FileCreateBlank,%file%
  TXTAddLine,%file%,"Hello World!",Append
End

RunEx,%ScriptFile%,Open-File,In=%file%,Out=%Return%
Message,"Open-File Terminated with code: %Return%"

[Open-File]
System,SetLocal
Echo,"Opening file: #1"
ShellExecute,Open,notepad.exe,#1
Set,#o1,%ExitCode%
System,EndLocal
```