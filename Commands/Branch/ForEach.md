# ForEach

Enumerates the elements of a list and executes its body for each element in the list.

## Syntax

```pebakery
ForEach,<%Variable%>,<List>,<Command>
```

```pebakery
ForEach,<%Variable%>,<List>,Begin
  <Command>
  ...
  <Command>
End
```

### Arguments

| Argument | Description |
| --- | --- |
| %Variable% | The variable to which an element will be assigned. |
| List | The list of items to enumerate. The list can be a variable or a string.|
| Delim= | **(Optional)** Delimiter used to separate the items in the list. Case Insensitive. **Default:** `\|` |
| Command | The command to be executed, or the `Begin` statement indicating a block of commands. |

## Remarks

ForEach statements may be nested.

At any point within the body of an ForEach statement, you can break out of the loop by using the `Break` statement, or step to the next iteration in the loop by using the `Continue` statement.

If the source list of the ForEach statement is empty, the body of the ForEach statement will not be executed. If `%Variable%` is uninitialized it will be `Nil`. If `%Variable%` is initialized, it's value will remain unchanged.

## Related

[Break](./Break.md), [Continue](./Continue.md)

## Examples

### Example 1

Enumerates and displays the elements in a list variable.

```pebakery
[Main]
Title=Simple ForEach Example
Description=Demonstrate how to perform a simple ForEach loop.
Level=5
Version=1
Author=Homes32

[Variables]
%EditionsList%=Home|Professional|Enterprise|Starter|Ultimate

[Process]
ForEach,%Edition%,%EditionsList%,Begin
    Message,"Edition is: %Edition%"
End
```

### Example 2

Enumerates and displays the elements in an in-line list.

```pebakery
[Main]
Title=Simple ForEach Example
Description=Demonstrate how to perform a simple ForEach loop.
Level=5
Version=1
Author=Homes32

[Variables]

[Process]
ForEach,%Fruit%,"Apples|Grapefruit|Kiwi|Oranges|Strawberries",Begin
    Message,"I like to eat: %Fruit%"
End
```