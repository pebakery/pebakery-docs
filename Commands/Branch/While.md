# While

Loops through a series of commands based on an expression.

## Syntax

```pebakery
While,<Expression>,<Command>
```

```pebakery
While,<Expression>,Begin
  <Command>
  ...
  <Command>
End
```

### Arguments

| Argument | Description |
| --- | --- |
| Expression | If the expression evaluates to true the following commands up to the `End` statement are executed. This loop continues until the expression evaluates to false. |
| Command | The command to be executed, or the `Begin` statement indicating a block of commands. |

## Remarks

While statements may be nested.

At any point within the body of an `While` statement, you can break out of the loop by using the `Break` statement, or step to the next iteration in the loop by using the `Continue` statement.

The expression is tested before the loop is executed so the loop will be executed zero or more times.

To create an infinite loop, you can use a fixed condition as the expression. (eg. `While,1,Equal,1`)

## Related

[Break](./Break.md), [Continue](./Continue.md)

## Examples

### Example 1

A simple loop that counts to 10 and displays a message box showing the current loop count.

```pebakery
[main]
Title=Simple While Example
Description=Demonstrate how to perform a simple While loop.
Level=5
Version=1
Author=Homes32

[variables]

[process]
Set,%i%,0
While,%i%,<=,10,Begin
  Message,"Value of i is: %i%"
  Math,Add,%i%,%i%,1
End
```
