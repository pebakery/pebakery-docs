# Math,ToChar

Converts an numerical code point to it's mapped character.

Code points usually represent a single grapheme—usually a letter, digit, punctuation mark, or whitespace—but sometimes represent symbols, control characters, or formatting.

## Syntax

```pebakery
Math,ToChar,<%DestVar%>,<CodePoint>
```

### Arguments

| Argument | Description |
| --- | --- |
| DestVar | The variable where the result will be stored. |
| CodePoint | The numerical code point to be converted to it's mapped character. |

### Control Characters

The following control characters are supported:

| Code | Description |
| --- | --- |
| 0x09 | `#$t` Tab |
| 0x0A | `#$x` Newline is converted to Carriage Return\Newline |

## Remarks

UCS-4 Unicode code points such as emoji are not supported at this time.

## Related

[FromChar](./FromChar.md)

## Examples

### Example 1

```pebakery
[Main]
Title=Math-ToChar Example
Description=Show usage of the Math,ToChar Command
Author=Homes32
Level=5

[Variables]

[Process]
// Control Char [Tab]
Math,ToChar,%result1%,0x09
// Printable Char [A]
Math,ToChar,%result2%,65
// Printable Char [|]
Math,ToChar,%result3%,0x7C
// Asian Char [가]
Math,ToChar,%result4%,0xAC00
// Asian Char [한]
Math,ToChar,%result5%,54620
// UCS-2 Symbol [★]
Math,ToChar,%result6%,0x2605
Message,"%result1%#$x%result2%#$x%result3%#$x%result4%#$x%result5%#$x%result6%#$x"
```

### Example 2

Advanced example using a `ForRange` loop to print out `A, B, C, ..., Z`.

```pebakery
[Main]
Title=Math-ToChar Example
Description=Show usage of the Math,ToChar Command
Author=ied206
Level=5

[Variables]

[Process]
Math,FromChar,%A%,A
Math,FromChar,%Z%,Z
Math,Add,%Z%,%Z%,1
ForRange,%i%,%A%,%Z%,1,Begin
  Math,ToChar,%ch%,%i%
  Echo,%ch%
End
```