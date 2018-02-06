# Web Label Control

A hyperlink that will open a webpage in the default browser.

## Syntax

```pebakery
<Name>=<Caption>,<Visibility>,10,<PosX>,<PosY>,<Width>,<Height>,<URL>[,<ToolTip>]
```

### Arguments

| Argument | Description |
| --- | --- |
| Name | Unique name used to reference this control. |
| Caption | Text displayed on the control. |
| Visibility | `True`/`False` - Show or Hide the control. |
| ControlID | The control ID specifying the type of the control. |
| PosX | Horizontal Position measured from the control's top left corner. |
| PosY | Vertical Position measured from the control's top left corner. |
| Width | Width of the control. |
| Height | Height of the control. |
| URL | The website to launch if the hyperlink is clicked. |
| ToolTip | **(Optional)** Help Text that will be shown when the user hovers over the control. This argument must always begin with a double underscore `__`. *Example:* `"__Some useful info"` |

## Remarks

PEBakery will always display the first 47 characters of the `URL` in the `ToolTip`.

## Related

[ReadInterface](/Commands/Interface/ReadInterface.md), [WriteInterface](/Commands/Interface/WriteInterface.md)

## Examples

```pebakery
// WebLabel
pWebLabel1=GitHub,1,10,250,160,32,18,https://github.com/
// WebLabel with ToolTip
pWebLabel1=GitHub,1,10,250,260,32,18,https://github.com/v/PEBakery"__Contribute to PEBakery's development."
```