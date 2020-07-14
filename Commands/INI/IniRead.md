# IniRead

Reads a value from a standard .ini file.

## Syntax

```pebakery
IniRead,<FileName>,<Section>,<Key>,<%DestVar%>[,Default=]
```

### Arguments

| Argument | Description |
| --- | --- |
| FileName | The full path of the file to read. |
| Section | The section containing the value to be read. |
| Key | The value to be read. |
| DestVar | The value will be saved to this variable. |
| Default= | **(Optional)** The value to be used if the Key cannot be found. If this parameter is NULL or undefined, the default is an empty string, "". |

## Remarks

PEBakery will optimize multiple `IniRead` commands in a row into a single read command.

## Example

Let's assume we have the following .ini file:

```pebakery
// C:\myFile.ini
[mySection]
myKey=myValue
anotherKey=anotherValue
```

### Example 1
In the following example the value of the key `myKey` will be stored inside `%myVariable%`.

```pebakery
IniRead,C:\myFile.ini,mySection,myKey,%myVariable%
```

### Example 2
In the following example the value of the key `myKey2` does not exist so the default value of `Hello` will be stored inside `%myVariable%`.

```pebakery
IniRead,C:\myFile.ini,mySection,myKey,%myVariable%,Default=Hello
```