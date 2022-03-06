# If

Conditionally run a statement.

## Syntax

```pebakery
If,<Condition>,<Command>
```

```pebakery
If,<Condition>,Begin
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

## Remarks

`If` statements and blocks can be nested.

## Related

[If-Else](./If-Else.md), [If-Question](./If-Question.md), [Operators](./Operators.md)

## Examples

### Example 1

```pebakery
[main]
Title=If Example
Description=Demonstrate how to run conditional statements using If.
Level=5
Version=1
Author=Homes32

[variables]

[process]
// Single If statement. Will create a text file if it doesn't already exist.
If,Not,ExistFile,C:\Temp\myFile.txt,FileCreateBlank,C:\Temp\myFile.txt

// If statement using a command block to run multiple commands if the statement evaluates to True.
If,ExistFile,C:\Temp\myFile.txt,Begin
  TXTAddLine,C:\Temp\myFile.txt,"Hello World!",APPEND
  ShellExecute,Open,C:\Temp\myFile.txt
End
```