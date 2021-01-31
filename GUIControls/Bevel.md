# Bevel Control

A rectangular frame used to organize controls.

## Syntax

```pebakery
<Name>=<Caption>,<Visibility>,12,<PosX>,<PosY>,<Width>,<Height>[,<FontSize>][,<FontWeight>][,<FontStyle>][,<ToolTip>]
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
| Font Style | **(Optional)** Can be `Italic`, `Underline`, `Strike`. |
| ToolTip | **(Optional)** Help Text that will be shown when the user hovers over the control. This argument must always begin with a double underscore `__`. *Example:* `"__Some useful info"` |

## Remarks

In order for the `Caption` to be displayed, a `Font Size` must be specified.

## Related

[ReadInterface](../Commands/Interface/ReadInterface.md), [WriteInterface](../Commands/Interface/WriteInterface.md)

## Examples

```pebakery
// Bevel with no caption (no Font Size specified)
Bevel1=Bevel1,1,12,128,8,414,287
Bevel2="",1,12,250,109,184,62

// Bevel with caption
Bevel3="Hello World!",1,12,250,19,104,82,10

// Bevel with 10pt font and Bold caption
Bevel4="Settings",1,12,135,239,400,50,10,Bold
```