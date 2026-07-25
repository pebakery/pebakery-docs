# List,Remove

Removes all occurrences of a value from a list. **Case Insensitive.**

## Syntax

```pebakery
List,Remove,<%ListVar%>,<Value>[,Delim=<Str>]
```

### Arguments

| Argument | Description |
| --- | --- |
| ListVar | The variable containing the list. |
| Value | The value to remove. |
| Delim= | **(Optional)** Delimiter used to separate the items in the list. Case Insensitive. **Default:** `\|` |

## Remarks

If the `Value` is not found `%ListVar%` will not be modified.

## Related

[List,RemoveAt](./RemoveAt.md), [List,RemoveX](./RemoveX.md)

## Examples

### Example 1

Remove _Ultimate_ from a list.

```pebakery
[Main]
Title=List-Remove Example 1
Description=Demonstrate usage of List,Remove.
Level=5
Version=1
Author=Homes32

[Variables]
%myList%=Home|UlTiMaTe|StarteR|Professional|Starter|Enterprise|PrOfEsSiOnAl|Starter|Ultimate

[Process]
List,Remove,%myList%,"Ultimate"
Message,"myList: %myList%"
```

### Example 2

This is an advanced example that demonstrates how we can remove duplicate items from a list.

```pebakery
[Main]
Title=List - Remove Duplicates Example
Description=Remove Duplicate items from a list. (Case Insensitive)
Level=5
Version=1
Author=Homes32

[Variables]
RemoveDuplicates=Run,%ScriptFile%,RemoveDups
%myList%=Professional|Home|professional|ultimate|Enterprise|Starter|Professional|starter|Ultimate

[Process]
Message,"myList: %myList%"
RemoveDuplicates,%myList%
Message,"Result: %myList%"

[RemoveDups]
// %^SIPARAM_1% - List
List,Count,%^SIPARAM_1%,%n%
Loop,%ScriptFile%,GetListItem-Loop,1,%n%,%^SIPARAM_1%
Set,%myList%,%tmpList%

[GetListItem-Loop]
// Loop through each item in the list.
// %^SIPARAM_1% - List
List,Get,%^SIPARAM_1%,%^LOOP_IDX%,%Item%
Run,%ScriptFile%,CheckListItem,%^SIPARAM_1%,%Item%

[CheckListItem]
// Check the value passed to determine if there are duplicates
// we test this by comparing the index of the first occurrence
// with the index of the last occurrence. If they are not equal
// that means we have multiple occurrences of the item.
// %^SIPARAM_1% - List  %^SIPARAM_2% - Item
List,Pos,%^SIPARAM_1%,%^SIPARAM_2%,%ItemFirstPos%
List,LastPos,%^SIPARAM_1%,%^SIPARAM_2%,%ItemLastPos%
If,Not,%ItemFirstPos%,Equal,%ItemLastPos%,Begin
  Echo,"Removing duplicate occurrences of [%Item%]..."
  // We don't care how many occurrences there are of %Item%
  // because we only want the 1st instance. This means
  // we can be lazy and just Remove all occurrences of %Item%
  // and not have to fool around looking for additional occurrences
  // between the 1st and the last.
  List,Remove,%^SIPARAM_1%,%^SIPARAM_2%
  // Then reinsert %Item% where we found the first occurrence
  List,Insert,%^SIPARAM_1%,%ItemFirstPos%,%^SIPARAM_2%
  // Run parameters are passed by value so
  // we need to return the result as a variable.
  Set,%tmpList%,%^SIPARAM_1%
  // Now that we have removed an item(s) our index count has changed
  // so we need break out of the current loop and restart to check
  // the remaining items in the list.
  Loop,Break
  Run,%ScriptFile%,RemoveDups,%tmpList%
End
```