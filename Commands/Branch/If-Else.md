# If-Else

Conditionally run statements.

## Syntax

```pebakery
If,<Condition>,<Command>
Else,<AltCommand>
```

```pebakery
If,<Condition>,Begin
 <Command>
 ...
 <Command>
End
Else,Begin
 <Command>
 ...
 <Command>
End
```

### Arguments

| Argument | Description |
| --- | --- |
| Condition | Condition to evaluate as `True` or `False`. |
| Command | The command to be executed if the condition is `True`. |
| AltCommand | The command to be executed if the condition is `False`. |

## Remarks

`If-Else` statements and blocks can be nested.

## Related

[If-Else](./If-Else.md), [If-Question](./If-Question.md)

## Examples

### Example 1

```pebakery
[main]
Title=If-Else Example
Description=Demonstrate how to run conditional statements using If-Else.
Level=5
Version=1
Author=Homes32

[variables]

[process]
// Single If-Else statement. Will create a text file if it doesn't already exist.
If,Not,ExistFile,C:\Temp\myFile.txt,Message,"File does not exist",INFORMATION
Else,Message,"File already exists",INFORMATION

// If-Else statement using a command block to run multiple commands.
If,ExistFile,C:\Temp\myFile.txt,Begin
  TXTAddLine,C:\Temp\myFile.txt,"Goodbye World!",APPEND
End
Else,Begin
  FileCreateBlank,C:\Temp\myFile.txt
  TXTAddLine,C:\Temp\myFile.txt,"Hello World!",APPEND
End

ShellExecute,Open,C:\Temp\myFile.txt
```