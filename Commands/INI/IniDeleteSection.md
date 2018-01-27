# IniDeleteSection

Deletes a section, along with all keys and values it contains from a standard .ini file.

## Syntax

```pebakery
IniDeleteSection,<Filename>,<Section>
```

### Arguments

| Argument | Description |
| --- | --- |
| FileName | The full path of the file. |
| Section | The Section to be removed. |

## Remarks

PEBakery will optimize multiple `IniDeleteSection` commands in a row to single delete command.

## Example

In the following example the section `mySection` will be removed along with any keys and values it contains.

```pebakery
IniDeleteSection,C:\myFile.ini,mySection
```
