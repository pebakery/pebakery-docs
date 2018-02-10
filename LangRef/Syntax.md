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

## Comments

Comments can be used to provide an explanation or annotation in the script in order to make it easier for other developers to understand what your script is doing. They can also be used to "comment out" lines of code while debugging a script.

PEBakery supports the C++ Style `//` comments as well as _.ini_ style comments using the hash `##` or semicolon `;` delimiters. Each comment must be placed on its own line and begin with a supported comment delimiter. A comment ends when a newline is started. PEBakery does not support multi-line "block" comments.

```text
// This is a comment
## This is also a comment
; This is another comment!
```

## Escape Characters

At times a comma, quote, or other reserved character may need to be used inside a string or parameter. In this situation the character must be "escaped".

| Escape Sequence | Character |
| --- | --- |
| #$c | Comma (,) |
| #$p | Percent (%) |
| #$q | Double quotes (") |
| #$s | Space |
| #$t | Tab |
| #$x | Newline (\r\n) |
| ##  | Hash mark (#) |

The `##` escape sequence is especially important to remember if you are performing an operation such as `IniWrite` or `RegWrite` that will write a string containing a `#` mark immediately followed by:

- the letter `a`, `r`, or `c`. - These tokens `#a` `#r` and `#c` are used by PEBakery to return special values when running loops or other sections within a script.
- a number `#12345`. - `#<integer>` are interpreted as PEBakery parameters.

Consider the following example:

```pebakery
[Main]
Title=Escapes Example
Author=Homes32
Level=5

[Variables]

[Process]
Run,%ScriptFile%,Test

[Test]
RegHiveLoad,Tmp_System,%RegSystem%

// Intended Result: HKLM\Tmp_System\ControlSet001\Control\CriticalDeviceDatabase\1394#609E&10483\Service
// Due to #609 being interpreted as a parameter
// Actual Result : HKLM\Tmp_System\ControlSet001\Control\CriticalDeviceDatabase\1394E&10483\Service
RegWrite,HKLM,0x1,Tmp_System\ControlSet001\Control\CriticalDeviceDatabase\1394#609E&10483,Service,sbp2port

// Use the escaped form of the # character `##`
// Result: HKLM\Tmp_System\ControlSet001\Control\CriticalDeviceDatabase\1394#609E&10483\Service
RegWrite,HKLM,0x1,Tmp_System\ControlSet001\Control\CriticalDeviceDatabase\1394##609E&10483,Service,sbp2port

RegHiveUnLoad,Tmp_System
```

## White Space

Strings containing white space must be enclosed in double quotes ("String with spaces").

PEBakery ignores white space at the beginning and end of lines, as well as blank lines. Where feasible, the use of blank lines is encouraged in order to keep your code organized and readable.
