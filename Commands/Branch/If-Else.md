# If-Else

Conditionally run statements.

## Syntax

### Single Statement

```pebakery
If,<Condition>,<Command>
Else,<AltCommand>
```

### Block Statement

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

### Single Statement Chain

```pebakery
If,<Condition>,<Command>
Else,If,<Condition>,<Command>
Else,If,<Condition>,<Command>
Else,If,<Condition>,<Command>
Else,If,<Condition>,<Command>
Else,<Condition>,<Command>
```

### Block Statement Chain

```pebakery
If,<Condition>,<Command>
Else,If,<Condition>,Begin
  <Command>
  ...
  <Command>
End  
Else,If,<Condition>,Begin
  <Command>
  ...
  <Command>
End
Else,If,<Condition>,Begin
  <Command>
  ...
  <Command>
End
Else,If,<Condition>,<Command>
Else,<Condition>,<Command>
```

### Arguments

| Argument | Description |
| --- | --- |
| Condition | Condition to evaluate as `True` or `False`. |
| Command | The command to be executed if the condition is `True`. |
| AltCommand | The command to be executed if the condition is `False`. |

## Remarks

`If-Else` statements and blocks may be nested and/or chained.

## Related

[If-Else](./If-Else.md), [If-Question](./If-Question.md), [Operators](./Operators.md)

## Examples

### Example 1

Simple If-Else statement to determine if a file exists.

```pebakery
[main]
Title=If-Else Example 1
Description=Demonstrate how to run conditional statements using If-Else.
Level=5
Version=1
Author=Homes32

[variables]

[process]
If,Not,ExistFile,C:\Temp\myFile.txt,Message,"File does not exist",INFORMATION
Else,Message,"File already exists",INFORMATION
```

### Example 2

If-Else statement using a command block to run multiple commands to create and/or write data to a file.

```pebakery
[main]
Title=If-Else Example 2
Description=Demonstrate how to run conditional statements using If-Else.
Level=5
Version=1
Author=Homes32

[variables]

[process]
If,ExistFile,C:\Temp\myFile.txt,Begin
  TXTAddLine,C:\Temp\myFile.txt,"Goodbye World!",APPEND
End
Else,Begin
  FileCreateBlank,C:\Temp\myFile.txt
  TXTAddLine,C:\Temp\myFile.txt,"Hello World!",APPEND
End

ShellExecute,Open,C:\Temp\myFile.txt
```

### Example 3

If-Else statement using a switch-like decision chain.

```pebakery
[main]
Title=If-Else Example 3
Description=Demonstrate how to run conditional statements using If-Else.
Level=5
Version=1
Author=Homes32

[variables]

[process]
Set,%i%,5

If,%i%,Equal,1,Message,1
Else,If,%i%,Equal,2,Message,2
Else,If,%i%,Equal,3,Message,3
Else,If,%i%,Equal,4,Message,4
Else,If,%i%,Equal,5,Message,5
Else,If,%i%,Equal,6,Message,6
Else,If,%i%,Equal,7,Message,7
Else,Message,"No Matches Found."
```

### Example 4

If-Else statement using a switch-like decision chain with blocks containing multiple commands.

```pebakery
[main]
Title=If-Else Example 4
Description=Demonstrate how to run conditional statements using If-Else.
Level=5
Version=1
Author=Homes32

[variables]

[process]
Set,%i%,5

If,%i%,Equal,1,Message,1
Else,If,%i%,Equal,2,Begin
  Message,2
  Echo,2
End
Else,If,%i%,Equal,3,Message,3
Else,If,%i%,Equal,4,Message,4
Else,If,%i%,Equal,5,Begin
  Message,5
  Echo,5
End
Else,If,%i%,Equal,6,Message,6
Else,If,%i%,Equal,7,Message,7
Else,Message,"No Matches Found."
```