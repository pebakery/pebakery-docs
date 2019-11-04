# Migrating from Winbuilder

Whether you have decided to take the plunge and migrate your entire project and/or scripts over to PEBakery, or you just want give PEBakery a trial run and experiment with your favorite project, here are a few things you need to consider.

## Backwards Compatibility

PEBakery was designed to be backwards compatible with Winbuilder 082's .script syntax for the express purpose of making it easy to migrate scripts and projects to the PEBakery platform. Most well designed scripts _should_ run without issues out of the box, however as with any complex application or project there may be exceptions.

**It is important to note that _Backwards Compatibility_ refers to the ability to run _most_ Winbuilder scripts in PEBakery and does not mean that scripts designed for PEBakery will continue to work in Winbuilder.**

## Caching

In order to reduce build and load times PEBakery reads all scripts into memory and caches them in a sql-lite database. This dramatically speeds up PEBakery but does require that you refresh the script each time changes are made to the physical script file. A running script cannot refresh itself, so this also means that new values set by commands such as `IniRead`/`IniWrite` will not update the script already in memory until the script or project is manually refreshed. 

Enhancements to PEBakery's interface handling, including the implementation of the `ReadInterface` and `WriteInterface` commands make using `Ini` commands to set script interface values completely unnecessary.

## Script Breaking Changes

This section contains a list of changes made during the development of PEBakery that will almost certainly break existing Winbuilder scripts. **Please read this section carefully when migrating.** If any of these changes affect you then you will need to modify your scripts.

### Compatibility Issues

Winbuilder has a number of bugs and unexpected behaviors, and over the years developers have implemented various workarounds to achieve the desired results in their projects. PEBakery has fixed the bugs that plagued Winbuilder, however some .scripts may still be written with the expectation that the bugs exist. In this case, the correctly functioning commands may produce different results then the author intended (like in the case of Winbuilder's ```DirCopy``` ```*.*``` bug). PEBakery has implemented various compatibility options allowing you to revert to the old buggy Winbuilder behavior while you update your scripts and make the transition to the PEBakery experience.

By default, PEBakery turns off all compatibility options in order to make Winbuilder bug fixes and enhancements immediately available for new scripts and projects.

Projects that meet the following criteria are encouraged to enable all Compatibility Options until it can be certified working under PEBakery.

- A project was designed and tested only with WinBuilder.
- A project was started in prior to 2017 (Pre-PEBakery era).
- A project that is distributed with the *WinBuilder.exe* executable (sometimes renamed *BuilderSE.exe*).

As of Feb 2019, the following projects require enabling various compatibility options:

- [ChrisPE](https://github.com/pebakery/chrispe)
- [MistyPE](http://mistyprojects.co.uk/documents/MistyPE/index.html)
- [Win10PESE](http://win10se.cwcodes.net/Compressed/index.php)
- [Win10XPE](http://win10se.cwcodes.net/Compressed/index.php)

#### Enabling Compatibility Options

To enable compatibility options repeat the following steps for each project. Compatibility settings are stored in a file called `PEBakeryCompat.ini`. This file must reside in the same directory as `script.project` (eg `Projects\Win10XPE\PEBakeryCompat.ini`).

1. Launch PEBakery, open `Settings`, and select the `Compat` tab.
1. Make sure the correct project is selected in the drop-down.
1. Click the `Select All` button.  
1. Save your changes.
1. **IMPORTANT**: Delete project temp files.

[A full list of compatibility options can be found here](/Usage/Settings-Compatibility.md)

#### Noteworthy Winbuilder Bugs

Some winbuilder bugs exist that are not covered by a compatibility option. Below is a non-exhaustive list of serious bugs that may require you to rewrite portions of your scripts.

| Bug | Description | Workaround |
| --- | --- | --- |
| Illegal characters in path | When performing path operations in Winbuilder such as `If,FileExist`, `If,DirExist` `ShellExecute` Winbuilder does not properly handle paths with illegal characters. | You must remove the illegal characters. |
| INIWrite Compact Behavior | Whenever Winbuilder performs an `IniWrite` or `Set,%someVar%,Permanent` command it will delete any contents found before the first section header in the file. It also strips comments beginning with the `;` character and extra whitespace, including spaces between key/value pairs (`key = value` becomes `key=value`. | If desired, PEBakery includes the `IniCompact` command, which can be used as a drop in compatibility measure to remove exra whitepsace including padding between key/value pairs. Simply add the line `If,%PEBakery%,Equal,True,IniCompact,<ScriptFile>` once to the beginning of your script. `IniCompact` will NOT remove comments or delete other code from your file. |

### Depreciated Commands

A handful Winbuilder commands and/or command arguments have been depreciated, if you have scripts that depend on these commands (which should be rare in modern projects) they will need to be updated before they will work in PEBakery.

For the most part depreciated commands fall into one of the following categories:

* Were created to work-around specific platform issues/limitations in Winbuilder's architecture. (eg. no x64 support, various Delphi bugs, no Unicode support, etc.) These workarounds are not necessary in PEBakery.
* Implemented for a specific use case or project that is no longer active. In many cases a better solution exists.
* Have no practical use case in PE building.
* Were completely broken in Winbuilder itself and therefore not used in any active projects.

[A full list of depreciated commands is maintained here](/Commands/Deprecated.md)

## Syntax Errors

In order to reduce the possibility for errors and unexpected behavior (that was notorious in Winbuilder) PEBakery includes a built-in syntax checker and utilizes a strict command parser. By default all scripts are automatically checked for errors whenever they are refreshed.

Because Winbuilder did not have a syntax checker and utilized a lazy parser that sometimes didn't even follow its own rules you may notice PEBakery complaining about errors in your script/project that seemed to work fine in Winbuilder (even though, by Winbuilder's own rules they are incorrect). These errors should be corrected to ensure the script always works the way it was intended to, both in PEBakery and Winbuilder.

### Common Syntax Errors in existing projects

#### Button Controls

Some buttons created in older versions of Winbuilder's internal interface editor omit the `Image` argument **and** suffer from duplicate `_SectionToRun_` and `ShowProgress` parameters. In this case you must update the control to include a value of `0` for the image argument or PEBakery will throw a syntax error. See the [Button Control](../GUIControls/Button.md) documentation for more details.

