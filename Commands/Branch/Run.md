# Run

Runs the commands found in a named `[Section]` of a script file.

You can run sections from any script including the script from where `Run` is originally called but only variables in the scope of the current script will be visible to the section being run.

## Syntax

```pebakery
Run,<FileName>,<Section>[,Parameters]
```

### Arguments

| Argument | Description |
| --- | --- |
| FileName | The full path of the script. Hint: Use %ScriptFile% to reference the current script. |
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

Although the parameters themselves are passed by value using tokens, all variables are in the scope of the entire script, so the original values can modified by referencing them by name. If required, you can use the `System,SetLocal` command to isolate variables modified within the running section.

## Related

[Exec](./Exec.md), [SetMacro](../Control/SetMacro.md), [System,SetLocal](../System/SetLocal.md), [System,EndLocal](../System/EndLocal.md)

## Examples

### Example 1

In this example we will use the `Run` command to organize code into sections that will be executed based on the value of a checkbox. This can be a useful alternative to `If-Else` command blocks if you have a large number of commands to run.

```pebakery
[Main]
Title=Run Example 1
Description=Show usage of the Run Command
Level=5
Version=1
Author=Homes32

[variables]

[process]
If,%pCheckBox1%,Equal,True,Run,%ScriptFile%,Register-Files
If,%pCheckBox2%,Equal,True,Run,%ScriptFile%,Copy-Files

[Register-Files]
// Do something...
Message,"Registering Files...",INFORMATION,5

[Copy-Files]
// Do something...
Message,"Copying Files...",INFORMATION,5

[Interface]
pCheckBox1="Register Some Files",1,3,10,14,143,18,False
pCheckBox2="Copy files",1,3,10,36,142,18,True
```

### Example 2

In this example we will use the `Run` command along with a parameter to execute a section.

```pebakery
[Main]
Title=Run Example 2
Description=Show usage of the Run Command with a parameter.
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

Run,%ScriptFile%,Open-File,%file%

[Open-File]
Echo,"Opening file: #1"
ShellExecute,Open,notepad.exe,#1
```