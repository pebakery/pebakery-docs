# File Box Control

An input box with a browse button that allows you to select a file or directory.

## Syntax

```pebakery
<Name>=<Value>,<Visibility>,13,<PosX>,<PosY>,<Width>,<Height>[,FLAG][,<ToolTip>]
```

### Arguments

| Argument | Description |
| --- | --- |
| Name | Unique name used to reference this control. |
| Value | The path currently entered in the File Box. |
| Visibility | `True`/`False` - Show or Hide the control. |
| ControlID | The control ID specifying the type of the control. |
| PosX | Horizontal Position measured from the control's top left corner. |
| PosY | Vertical Position measured from the control's top left corner. |
| Width | Width of the control. |
| Height | Height of the control. |
| ToolTip | **(Optional)** Help Text that will be shown when the user hovers over the control. This argument must always begin with a double underscore `__`. *Example:* `"__Some useful info"` |

### Flags

The following flags are mutually exclusive.

| Argument | Description |
| --- | --- |
| DIR | **(Default)** The browse button will display a directory selection dialog. |
| FILE | The browse button will display a file selection dialog. |

## Remarks

The `Value` of the File Box can be read by referencing the control `Name` as a variable. Ex. `%FileBox1%` or by using the `ReadInterface` command.

## Related

[ReadInterface](/Commands/Interface/ReadInterface.md), [WriteInterface](/Commands/Interface/WriteInterface.md)

## Examples

```pebakery
//Select a file
FileBox1=,1,13,330,219,172,20,file

// Select a directory
FileBox2=,1,13,330,262,172,20,dir
```