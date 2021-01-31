# StrFormat,Date

Returns the current Date and Time in the specified format.

## Syntax

```pebakery
StrFormat,Date,<%DestVar%>,<FormatString>
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
| g | Gregorian Era | display  `B.C.` or `A.D.` |
| AM/PM | Displays the time in 12hr format. | `hh:nn AM/PM`
| : / - . | date/time separator |

## Remarks

PEBakery returns all date/time formats using Invariant Culture.

## Related

## Examples

### Example 1

```pebakery
[Main]
Title=StrFormat-Date
Description=Show the usage of StrFormat,Date.
Level=5
Version=1
Author=Homes32

[Variables]

[Process]
// Common Date Formats
StrFormat,date,%longDate1%,"dddd, MMMM dd, yyyy"
StrFormat,date,%longDate2%,"ddd, MMM dd, yyy"
StrFormat,date,%shortDate1%,"yyyy-mm-dd"
StrFormat,date,%shortDate2%,"mm/dd/yyy"
// Common Time Formats
StrFormat,date,%time1%,"hh:nn"
StrFormat,date,%time2%,"hh:nn:ss"
StrFormat,date,%time3%,"hh:nn:ss:z"
StrFormat,date,%time4%,"hh:nn AM/PM"
StrFormat,date,%time5%,"yyyy-mm-dd hh:nn AM/PM"
StrFormat,date,%time6%,"t"
StrFormat,date,%time7%,"tt"
StrFormat,date,%datetime%,"dddd, MMMM dd, yyyy hh:nn:ss"
Message,"%longDate1%#$x%longDate2%#$x%shortDate1%#$x%shortDate2%#$x#$x%time1%#$x%time2%#$x%time3%#$x%time4%#$x%time5%#$x%time6%#$x%time7%#$x%datetime%"
```