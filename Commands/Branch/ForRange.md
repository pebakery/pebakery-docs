# ForRange

Loops through a series of commands based on the value of a counter.

## Syntax

```pebakery
ForRange,<%Variable%>,<Start>,<End>,<Step>,<Command>
```

```pebakery
ForRange,<%Variable%>,<Start>,<End>,<Step>,Begin
  <Command>
  ...
  <Command>
End
```

### Arguments

| Argument | Description |
| --- | --- |
| %Variable% | The variable used for the loop count. |
| Start | The starting value of `%Variable%`. (Integer) |
| End |  The ending value of `%Variable%`. (Integer) |
| Step | Decrement/Increment by this value until the `End` count is reached. (Integer) |
| Command | The command to be executed, or the `Begin` statement indicating a block of commands. |

## Remarks

ForRange statements may be nested.

At any point within the body of an ForRange statement, you can break out of the loop by using the `Break` statement, or step to the next iteration in the loop by using the `Continue` statement.

The ForRange loop terminates when the value of `%Variable%` exceeds the `End` threshold. If `Step` or `End` is a variable, its value is only read the first time the loop executes.

A ForRange loop will execute zero times if `Start` <= `End` and `Step` is negative

If `Start` > `End` and `Step` > 0 the command will Halt the build to avoid an infinite loop condition.

## Related

[Break](./Break.md), [Continue](./Continue.md), [Loop](./Loop.md), [LoopEx](./LoopEx.md), [LoopLetter](./LoopLetter.md)

## Examples

### Example 1

Countdown from 5 to 0.

```pebakery
[Main]
Title=Simple ForRange Example
Description=Demonstrate how to perform a simple ForRange loop.
Level=5
Version=1
Author=Homes32

[Variables]

[Process]
ForRange,%i%,5,0,-1,Begin
    Message,"Countdown: %i%"
End
```

### Example 2

Count to 10, using variables for `Start`, `End`, `Step`.

```pebakery
[Main]
Title=Simple ForRange Example
Description=Demonstrate how to perform a simple ForRange loop.
Level=5
Version=1
Author=Homes32

[Variables]
%Start%=1
%End%=11
%Step%=1

[Process]
ForRange,%i%,%Start%,%End%,%Step%,Begin
    Message,"%i%"
End
```
