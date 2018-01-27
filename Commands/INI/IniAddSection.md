# IniAddSection

Adds a new empty section inside a standard .ini file.

## Syntax

```pebakery
IniAddSection,<FileName>,<Section>
```

### Arguments

| Argument | Description |
| --- | --- |
| FileName | The full path of the file. |
| Section | The name of the Section to be added. |

## Remarks

If the section already exists no action will be taken.

PEBakery will optimize multiple `IniAddSection` in a row to single command.

## Example

In the following example the section `mySection` will be created inside C:\myFile.ini.

```pebakery
IniAddSection,C:\myFile.ini,mySection
```
