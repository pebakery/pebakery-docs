# IniReadSection

Reads the contents of a section in a standard .ini file and outputs the result as a list structure.

The string returned is a 1-dimensional list with the `Keys` in the Odd position and the `Values` in the even position.

## Syntax

```pebakery
IniReadSection,<FileName>,<Section>,<%DestVar%>[,Delim=<str>]
```

### Arguments

| Argument | Description |
| --- | --- |
| FileName | The full path of the file to read. |
| Section | The section to be read. |
| DestVar | The value will be saved to this variable. |
| Delim= | **(Optional)** Delimiter used to separate the `Items` in the list. **Default:** `\|` |

## Remarks

Note: Special characters such as comma's `,` must be escaped `#$c` when specifying the `Delim=` argument.

PEBakery will optimize multiple `IniReadSection` commands in a row to single read command.

## Example

Let's assume a file `%SrcFile%` contains these lines:

```pebakery
[English]
1=One
2=Two
3=Three

[Korean]
1=하나
2=둘
```

### Example 1

In the following example the contents of the section `English` will be stored inside `%Dest%`.

```pebakery
IniReadSection,%SrcFile%,English,%Dest%
```

Returns:

```pebakery
1|One|2|Two|3|Three
```

### Example 2

IniReadSection will return the section `Korean` into `%Dest%`.

```pebakery
IniReadSection,%SrcFile%,Korean,%Dest%,Delim=#$c
```

Returns:

```pebakery
1,하나,2,둘
```