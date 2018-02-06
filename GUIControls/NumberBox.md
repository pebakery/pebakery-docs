# Number Box Control

An input box that accepts a number between a given minimum and maximum range.

## Syntax

```pebakery
<Name>=<Name>,<Visibility>,2,<PosX>,<PosY>,<Width>,<Height>,<Value>,<Min>,<Max>,<Increment>[,<ToolTip>]
```

### Arguments

| Argument | Description |
| --- | --- |
| Name | Unique name used to reference this control. |
| Visibility | `True`/`False` - Show or Hide the control. |
| ControlID | The control ID specifying the type of the control. |
| PosX | Horizontal Position measured from the control's top left corner. |
| PosY | Vertical Position measured from the control's top left corner. |
| Width | Width of the control. |
| Height | Height of the control. |
| Min | The minimum value the number box will allow. |
| Max | The maximum value the number box will allow. |
| Increment | Clicking the up/down arrows on the number box will increase the value by a factor of X. |
| ToolTip | **(Optional)** Help Text that will be shown when the user hovers over the control. This argument must always begin with a double underscore `__`. *Example:* `"__Some useful info"` |

## Remarks

## Related

[ReadInterface](/Commands/Interface/ReadInterface.md), [WriteInterface](/Commands/Interface/WriteInterface.md)

## Examples

```pebakery
NumberBox1=pNumberBox1,1,2,473,31,56,22,0,0,256,1,"__Increment positive number by a factor of 1"
NumberBox2=pNumberBox2,1,2,473,60,55,22,0,-256,256,2,"__Increment or decrement number by a factor of 2"
```