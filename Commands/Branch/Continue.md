# Continue

Continue execution of a While/ForEach/ForRange loop.

## Syntax

```pebakery
Continue
```

### Arguments

None.

## Remarks

Continue will continue execution of the loop from the original While/ForEach/ForRange statement.

ContinueLoop can be rewritten using If-ElseIf-EndIf statements, however using ContinueLoop can make long scripts easier to understand.

Be careful using Continue with While loops; you can create infinite loops by using Continue incorrectly.

## Related

[Break](./Break.md), [ForEach](./ForEach.md), [ForRange](./ForRange.md), [While](./While.md)

## Examples

### Example 1

Count upward from 1 to 10 but skip displaying 5.

```pebakery
[Main]
Title=Simple Continue Example
Description=Demonstrate how to Continue a loop.
Level=5
Version=1
Author=Homes32

[Variables]

[Process]
ForRange,%i%,1,11,1,Begin
  If,%i%,Equal,5,Continue
  Message,"#$pi#$p: %i%"
End
```
