# .Script Command Syntax

PEBakery projects and scripts are written using a scripting language tailored to building bootable Pre-Install (PE) environments.

PEBakery's scripting engine provides native commands for common tasks such as:

- copying files & directories
- downloading files
- extracting archives (.zip, .7z, etc.)
- modifying registry hives
- reading and writing configuration files
- string manipulation
- working with WIM files

Advanced functionality includes the ability to define macros and execute external processes, giving you virtually unlimited potential to customize and extend a scripts functionality using external tools such as the Windows command prompt, powershell, AutoIt3, or standalone applications.

## Syntax

PEBakery commands consist of a keyword followed by one or more parameters separated by commas. The commands are organized into "sections" similar to a standard _.ini_ file.

## Escape Characters

At times a comma, quote, or other reserved character may need to be used inside a string or parameter. In this situation the character must be "escaped".

| Escape Sequence | Character |
| --- | --- |
| #$c | Comma (,) |
| #$h | Hash mark (#) |
| #$p | Percent (%) |
| #$q | Double quotes (") |
| #$s | Space |
| #$t | Tab |
| #$x | Newline (\r\n) |

## White Space

Strings containing white space must be enclosed in double quotes ("String with spaces").

PEBakery ignores white space at the beginning and end of lines and parameters. Blank lines are also ignored. Where feasible, the use of white space is encouraged in order to keep your code organized and readable.
