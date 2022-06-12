# Break

Terminate execution of a While/ForEach/ForRange loop.

## Syntax

```pebakery
Break
```

### Arguments

None.

## Remarks

Breaking out of a loop will continue execution of the script with the next line following the end of the While/ForEach/ForRange statement.

## Related

[Continue](./Continue.md), [ForEach](./ForEach.md), [ForRange](./ForRange.md), [While](./While.md)

## Examples

### Example 1

Break out of an infinite loop with a certain condition occurs.

```pebakery
[Main]
Title=Simple Break Example
Description=Demonstrate how to Break out of a loop.
Level=5
Version=1
Author=Homes32

[Variables]

[Process]

Set,%i%,0

; Infinite loop
While,1,Equal,1,Begin
  Message,"i = %i%"
  If,%i%,Equal,5,Break
  Math,Add,%i%,%i%,1
End
```
