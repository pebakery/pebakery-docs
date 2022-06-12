# Math,FromChar

Converts an mapped character to it's numerical code point (in Hex).

Code points usually represent a single grapheme—usually a letter, digit, punctuation mark, or whitespace—but sometimes represent symbols, control characters, or formatting.

## Syntax

```pebakery
Math,FromChar,<%DestVar%>,<Char>
```

### Arguments

| Argument | Description |
| --- | --- |
| DestVar | The variable where the result will be stored. |
| Char | The to be converted to numerical code point. |

### Control Characters

The following control characters are supported:

| Code | Description |
| --- | --- |
| `#$t` | `0x09` Tab |
| `#$x` | `0x0A` Carriage Return\Newline |

## Remarks

UCS-4 Unicode code points such as emoji are not supported at this time.

## Related

[ToChar](./ToChar.md)

## Examples

### Example 1

```pebakery
[Main]
Title=Math-FromChar Example
Description=Show usage of the Math,FromChar Command
Author=Homes32
Level=5

[Variables]

[Process]
// Control Char [0x09]
Math,FromChar,%result1%,"#$t"
// Printable Char [0x41]
Math,FromChar,%result2%,"A"
// Printable Char [0x7C]
Math,FromChar,%result3%,"|"
// Asian Char [0xAC00]
Math,FromChar,%result4%,"가"
// Asian Char [0xD55C]
Math,FromChar,%result5%,"한"
// UCS-2 Symbol [0x2605★]
Math,FromChar,%result6%,"★"
Message,"%result1%#$x%result2%#$x%result3%#$x%result4%#$x%result5%#$x%result6%#$x"
```

### Example 2

Advanced example using a `ForRange` loop to print out `A, B, C, ..., Z`.

```pebakery
[Main]
Title=Math-FromChar Example
Description=Show usage of the Math,FromChar Command
Author=ied206
Level=5

[Variables]

[Process]
Math,FromChar,%A%,A
Math,FromChar,%Z%,Z
Math,Add,%Z%,%Z%,1
ForRange,%i%,%A%,%Z%,1,Begin
  Math,FromChar,%ch%,%i%
  Echo,%ch%
End
```