# File Box Control

An input box with a browse button that allows you to select a file or directory.

## Syntax

```pebakery
<Name>=<Value>,<Visibility>,13,<PosX>,<PosY>,<Width>,<Height>[,<Type>][,Title=<Text>][,Filter=<FilterString>][,<ToolTip>]
```

### Arguments

| Argument | Description |
| --- | --- |
| Name | Unique name used to reference this control. |
| Value | The path currently entered in the File Box. |
| Visibility | `True`/`False` - Show or Hide the control. |
| ControlID | `13` - The control ID specifying that this is a File Box. |
| PosX | Horizontal Position measured from the control's top left corner. |
| PosY | Vertical Position measured from the control's top left corner. |
| Width | Width of the control. |
| Height | Height of the control. |
| Type   | **(Optional)** Dialog type must be one of the following: |
|| `DIR` - **(Default)** The browse button will display a directory selection dialog. |
|| `FILE` - The browse button will display a file selection dialog. |
| Title= | **(Optional)** Text that will be displayed in the dialog title bar. **(Default)** |
| Filter= | **(Optional)** A filter string used to restrict the file type a user may choose. **(File Browser Only)** |
| ToolTip | **(Optional)** Help Text that will be shown when the user hovers over the control. This argument must always begin with a double underscore `__`. *Example:* `"__Some useful info"` |

Optional arguments may be specified in any order.

## File Filter

You may force the user to pick from specific file types (ie. *.ini;*.txt;*.cfg file) by specifying `Filter=` argument.

For each filtering option, the filter string contains a description of the filter, followed by the vertical bar (|) and the filter pattern. The strings for different filtering options are separated by the vertical bar.

The following is an example of a filter string:

`Text files|*.txt|All files|*.*`

You can add several filter patterns to a filter by separating the file types with semicolons, for example:

`Image files|*.BMP;*.JPG;*.GIF|All files (*.*)|*.*`

The filter order is defined by the order of the filter list, therefore the first filter in the list will be the default selected filtering option.

## Remarks

The `Value` of the File Box can be read by referencing the control `Name` as a variable. Ex. `%FileBox1%` or by using the `ReadInterface` command.

## Related

[PathBox](./PathBox.md), [ReadInterface](../Commands/Interface/ReadInterface.md), [WriteInterface](../Commands/Interface/WriteInterface.md)

## Examples

```pebakery
// Select a file
FileBox1=,1,13,330,219,172,20,file
FileBox2=,1,13,330,219,172,20,file,"Title=Please select another file"

// Select a file, using the `Filter=` argument to only allow the user to pick ini/cfg files by default.
FileBox1=,1,13,330,219,172,20,file,"Filter=Config Files|*.ini;*.cfg|All Files|*.*"

// Select a directory
FileBox2=,1,13,330,262,172,20,dir

```