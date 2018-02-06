# Text Label Control

Displays a line of text.

## Syntax

```pebakery
<Name>=<Caption>,<Visibility>,1,<PosX>,<PosY>,<Width>,<Height>,<FontSize>,<FontWeight>[,<ToolTip>]
```

### Arguments

| Argument | Description |
| --- | --- |
| Name | Unique name used to reference this control. |
| Caption | Text displayed on the control. |
| Visibility | `True`/`False` - Show or Hide the control. |
| ControlID | `1` - The control ID specifying that this is a Text Label. |
| PosX | Horizontal Position measured from the control's top left corner. |
| PosY | Vertical Position measured from the control's top left corner. |
| Width | Width of the control. |
| Height | Height of the control. |
| Font Size | Font Size in points. (ex. 12) |
| Font Weight | Can be `Normal`, `Bold`, `Italic`, `Underline`, or `Strike`. |
| ToolTip | **(Optional)** Help Text that will be shown when the user hovers over the control. This argument must always begin with a double underscore `__`. *Example:* `"__Some useful info"` |

## Remarks

Text labels will wrap text, allowing multiple lines to be displayed within the `Width` and `Height` boundary of the Text Label.

## Related

[ReadInterface](/Commands/Interface/ReadInterface.md), [WriteInterface](/Commands/Interface/WriteInterface.md)

## Examples

```pebakery
pTextLabel1="Hello World!",1,1,20,50,230,18,8,Normal
```