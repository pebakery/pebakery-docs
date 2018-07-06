# List,RemoveX

Removes all occurrences of a value from a list. **Case Sensitive.**

## Syntax

```pebakery
List,RemoveX,<%ListVar%>,<Value>[,Delim=<Str>]
```

### Arguments

| Argument | Description |
| --- | --- |
| ListVar | The variable containing the list. |
| Value | The value to remove. |
| Delim= | **(Optional)** Delimiter used to separate the items in the list. **Default:** `\|` |

## Remarks

If the `Value` is not found `%ListVar%` will not be modified.

## Related

[List,Remove](./RemoveX.md), [List,RemoveAt](./RemoveAt.md)

## Examples

### Example 1

Remove _Starter_ from a list.

```pebakery
[Main]
Title=List-RemoveX Example 1
Description=Demonstrate usage of List,RemoveX.
Level=5
Version=1
Author=Homes32

[Variables]
%myList%=Home|UlTiMaTe|StarteR|Professional|Starter|Enterprise|PrOfEsSiOnAl|Starter|Ultimate

[Process]
List,RemoveX,%myList%,"Starter"
Message,"myList: %myList%"
```

### Example 2

This is an advanced example that demonstrates how we can remove duplicate items from a list.

```pebakery
[Main]
Title=List - Remove DuplicatesX Example
Description=Remove Duplicate items from a list. (Case Sensitive)
Level=5
Version=1
Author=Homes32

[Variables]
RemoveDuplicatesX=Run,%ScriptFile%,RemoveDupsX
%myList%=Professional|Home|professional|ultimate|Enterprise|Starter|Professional|starter|Ultimate

[Process]
Message,"myList: %myList%"
RemoveDuplicatesX,%myList%
Message,"Result: %myList%"

[RemoveDupsX]
// #1 - List
List,Count,#1,%n%
Loop,%ScriptFile%,GetListItemX-Loop,1,%n%,#1
Set,%myList%,%tmpList%

[GetListItemX-Loop]
// Loop through each item in the list.
// #1 - List
List,Get,#1,#c,%Item%
Run,%ScriptFile%,CheckListItemX,#1,%Item%

[CheckListItemX]
// Check the value passed to determine if there are duplicates
// we test this by comparing the index of the first occurrence
// with the index of the last occurrence. If they are not equal
// that means we have multiple occurrences of the item.
// #1 - List  #2 - Item
List,PosX,#1,#2,%ItemFirstPosX%
List,LastPosX,#1,#2,%ItemLastPosX%
If,Not,%ItemFirstPosX%,Equal,%ItemLastPosX%,Begin
  Echo,"Removing duplicate occurrences of [%Item%]..."
  // We don't care how many occurrences there are of %Item%
  // because we only want the 1st instance. This means
  // we can be lazy and just Remove all occurrences of %Item%
  // and not have to fool around looking for additional occurrences
  // between the 1st and the last.
  List,RemoveX,#1,#2
  // Then reinsert %Item% where we found the first occurrence
  List,Insert,#1,%ItemFirstPosX%,#2
  // Run parameters are passed by value so
  // we need to return the result as a variable.
  Set,%tmpList%,#1
  // Now that we have removed an item(s) our index count has changed
  // so we need break out of the current loop and restart to check
  // the remaining items in the list.
  Loop,Break
  Run,%ScriptFile%,RemoveDupsX,%tmpList%
End
```