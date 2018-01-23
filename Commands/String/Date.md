# StrFormat,Date

Returns the current Date and Time in the specified format.

This command uses Winbuilder's Date/Time formatting rules. For Date/Time formatting using Standard Formatting options use `StrFormat,DateTime`.

## Syntax

```pebakery
StrFormat,Round,<%DestVar%>,<FormatString>
```

### Arguments

| Argument | Description |
| --- | --- |
| DestVar | Variable where the result will be stored. |
| FormatString | The format string for the date/time. |

### Winbuilder Date/Time Format Strings

| Format specifier | Description | Examples |
| --- | --- | --- |
| d | Day of the Week | `d` - day<br/>`dd` - day including any leading zeros<br/>`ddd` - 3 letter Day<br/>`dddd` - Full day |
| m | Month | `m` - month<br/>`mm` - month including any leading zeros<br/>`mmm` - 3 letter month<br/>`mmmm` - Full month |
| y | Year | `y` - 2 digit year<br/>`yy` - 2 digit year<br/>`yyyy` - 4 digit year |
| h | Hours | `h` - hour of the day<br/>`hh` - hour of the day including any leading zeros |
| n | Minutes | `n` - minutes<br/>`nn` - minutes including any leading zeros |
| s | Seconds | `s` - seconds<br/>`ss` - seconds including any leading zeros |
| z | Milliseconds | `z` - milliseconds |
| t | Time (12 hr format) | `t` - Short 12hr time Ex. *2:13 PM*<br/>`tt` - Long 12hr time. Ex. *2:13:25 PM* |
| g | Era | display  `B.C.` or `A.D.` |
| AM/PM | Displays the time in 12hr format. | `hh:nn AM/PM`

## Remarks

## Related

[StrFormat,DateTime](./DateTime.md)

## Examples

### Example 1

```pebakery

```