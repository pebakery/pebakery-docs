# Bevel Control

A rectangular frame used to organize controls.

## Syntax

```pebakery
<Name>=<Caption>,<Visibility>,12,<PosX>,<PosY>,<Width>,<Height>[,<FontSize>][,<FontWeight>][,<ToolTip>]
```

### Arguments

| Argument | Description |
| --- | --- |
| Name | Unique name used to reference this control. |
| Caption | Label displayed on the top of the bevel. Use `""` for none. |
| Visibility | `True`/`False` - Show or Hide the control. |
| ControlID | `12` - The control ID specifying that this is a Bevel. |
| PosX | Horizontal Position measured from the control's top left corner. |
| PosY | Vertical Position measured from the control's top left corner. |
| Width | Width of the control. |
| Height | Height of the control. |
| Font Size | **(Optional)** Font Size in points. (ex. 12) |
| Font Weight | **(Optional)** Can be `Normal`, `Bold`. |
| ToolTip | **(Optional)** Help Text that will be shown when the user hovers over the control. This argument must always begin with a double underscore `__`. *Example:* `"__Some useful info"` |

## Remarks

For backwards compatibility with interfaces designed using Winbuilder's internal editor, if the control `Name` is equal to the `Caption` argument no caption will be shown.

In order for the `Caption` to display, the compatibility option *Disable Bevel Caption* must be disabled in PEBakery's settings.

## Related

[ReadInterface](/Commands/Interface/ReadInterface.md), [WriteInterface](/Commands/Interface/WriteInterface.md)

## Examples

```pebakery
// Bevel with no caption
Bevel1=Bevel1,1,12,128,8,414,287
Bevel2="",1,12,250,109,184,62,10,Bold

// Bevel with caption
Bevel3="Hello World!",1,12,250,19,104,82

// Bevel with 10pt font and Bold caption
Bevel4="Settings",1,12,135,239,400,50,10,Bold
```