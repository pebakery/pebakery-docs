# File Box Control

An input box with a browse button that allows you to select a file or directory.

## Syntax

```pebakery
<Name>=<Value>,<Visibility>,13,<PosX>,<PosY>,<Width>,<Height>[,FLAG][,<ToolTip>][,Title=<Text>]
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
| ToolTip | **(Optional)** Help Text that will be shown when the user hovers over the control. This argument must always begin with a double underscore `__`. *Example:* `"__Some useful info"` |
| Title= | **(Optional)** Text that will be displayed in the dialog's title bar. **(Default)** If this argument is not defined the title bar will display `Open` (FilePath) or `Select Folder` (DirPath). |

Optional arguments may be specified in any order.

### Flags

The following flags are mutually exclusive.

| Argument | Description |
| --- | --- |
| DIR | **(Default)** The browse button will display a directory selection dialog. |
| FILE | The browse button will display a file selection dialog. |

## Remarks

The `Value` of the File Box can be read by referencing the control `Name` as a variable. Ex. `%FileBox1%` or by using the `ReadInterface` command.

## Related

[ReadInterface](../Commands/Interface/ReadInterface.md), [WriteInterface](../Commands/Interface/WriteInterface.md)

## Examples

```pebakery
//Select a file
FileBox1=,1,13,330,219,172,20,file
FileBox2=,1,13,330,219,172,20,file,"Title=Please select another file"

// Select a directory
FileBox2=,1,13,330,262,172,20,dir
```