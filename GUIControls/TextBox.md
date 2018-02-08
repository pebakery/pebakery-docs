# Text Box Control

An input box that accepts a single line of text.

## Syntax

```pebakery
<Name>=<Caption>,<Visibility>,0,<PosX>,<PosY>,<Width>,<Height>,<Value>[,<ToolTip>]
```

### Arguments

| Argument | Description |
| --- | --- |
| Name | Unique name used to reference this control. |
| Caption | The Label displayed over the text box. Use `""` for none. |
| Visibility | `True`/`False` - Show or Hide the control. |
| ControlID | `0` - The control ID specifying that this is a Text Box. |
| PosX | Horizontal Position measured from the control's top left corner. |
| PosY | Vertical Position measured from the control's top left corner. |
| Width | Width of the control. |
| Height | Height of the control. |
| Value | The value of the text box. |
| ToolTip | **(Optional)** Help Text that will be shown when the user hovers over the control. This argument must always begin with a double underscore `__`. *Example:* `"__Some useful info"` |

## Remarks

The `Value` of the text box can be read by referencing the control `Name` as a variable. Ex. `%TextBox1%` or by using the `ReadInterface` command.

## Related

[ReadInterface](/Commands/Interface/ReadInterface.md), [WriteInterface](/Commands/Interface/WriteInterface.md)

## Examples

```pebakery
TextBox1=TextBox,1,0,138,179,171,21,"abc.."
```