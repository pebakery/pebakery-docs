# List Commands

List commands allow you to create and manipulate list structures.

A PEBakery `List` consists of a one dimensional array of strings separated by a chosen delimiter. The first element of the array is indexed by subscript of 1 (1-based index) and incremented for each additional item in the list.

Example:

```pebakery
%myList%=Home|Professional|Enterprise|Starter|Ultimate
```

Translates logically into:

| | | | | | |
| --- | :---: | :---: | :---: | :---: | :---: |
| **Index** | 1 | 2 | 3 | 4 | 5 |
| **Value** | Home | Professional | Enterprise | Starter | Ultimate |

Click on a Command name for a detailed description.

| Command | Description |
| --- | --- |
| [List,Append](./Append.md) | Append a value to the end of a list. |
| [List,Count](./Count.md) | Returns the number of items in a list. |
| [List,Get](./Get.md) | Extracts a specific item from a list. |
| [List,Insert](./Insert.md) | Insert a new value into a specific location in a list. |
| [List,LastPos](./LastPos.md) | Returns the last position of the given value inside the specified list. **Case Insensitive.** |
| [List,LastPosX](./LastPosX.md) | Returns the last position of the given value inside the specified list. **Case Sensitive.** |
| [List,Pos](./Pos.md) | Returns the position of the given value inside the specified list. **Case Insensitive.** |
| [List,PosX](./PosX.md) | Returns the position of the given value inside the specified list. **Case Sensitive.** |
| [List,Remove](./Remove.md) | Removes all occurrences of a value from a list. **Case Insensitive.** |
| [List,RemoveAt](./RemoveAt.md) | Removes a value from a specific index in a list. |
| [List,RemoveX](./RemoveX.md) | Removes all occurrences of a value from a list. **Case Sensitive.** |
| [List,Set](./Set.md) | Writes a value to a specific index in a list. |
| [List,Sort](./Sort.md) | Sorts a list into alphabetical/lexicographical order. **Case Insensitive.** |
| [List,SortN](./SortN.md) | Sorts a list into natural order. **Case Insensitive.** |
| [List,SortNX](./SortNX.md) | Sorts a list into natural order. **Case Sensitive.** |
| [List,SortX](./SortX.md)  | Sorts a list into alphabetical/lexicographical order. **Case Sensitive.** |
