# Migrating from Winbuilder

So, you have decided to migrate your project and/or scripts over to PEBakery. Great! Here are a few things you need to consider.

## Backwards Compatibility

PEBakery was designed to be backwards compatible with Winbuilder 082's .script syntax for the express purpose of making it easy to migrate scripts and projects to the PEBakery platform. Most well designed scripts _should_ run without issues out of the box, however as with any complex application there a couple exceptions.

**It is important to note that _Backwards Compatibility_ refers to the ability to run _most_ Winbuilder scripts in PEBakery and does not mean that scripts designed for PEBakery will continue to work in Winbuilder.**

## Caching

In order to reduce build and load times PEBakery reads all scripts into memory and caches them in a sql-lite database. This dramatically speeds up PEBakery but does require that you refresh the script each time changes are made to the physical script file. A running script cannot refresh itself, so this also means that new values set by commands such as `IniRead`/`IniWrite` will not update the script already in memory until the script or project is manually refreshed. Enhancements to PEBakery's interface handling including the implementation of the `ReadInterface` and `WriteInterface` commands make using `Ini` commands to set script interface values completely unnecessary.

## Depreciated Commands

A handful Winbuilder commands have been depreciated, if you have scripts that depend on these commands (which should be rare in modern projects) they will need to be updated before they will work in PEBakery.

For the most part deprecated commands fall into the following categories:

* Worked around specific platform issues/limitations in Winbuilder's architecture. (eg. no x64 support, Delphi bugs, etc.) These workarounds are not necessary in PEBakery.
* Implemented for a specific use case or project that is no longer active and/or better solutions now exist.
* Have no practical use case in PE building.
* Were completely broken in Winbuilder itself and not used in any active projects.

[A full list of depreciated commands is maintained here](/Commands/Depreciated.md).

## Compatibility Issues

Winbuilder has a number of bugs and unexpected behavior and over the years developers have learned to work around the bugs and quirks. PEBakery has fixed the bugs that plagued Winbuilder, however some .scripts may still be written with the expectation that the bugs exist. In this case, the correctly functioning commands may produce different results then the author intended (like in the case of Winbuilder's ```DirCopy``` ```*.*``` bug). PEBakery has implemented several compatibility options allowing you to revert to the old buggy Winbuilder behavior while you rewrite your scripts and make the transition to the PEBakery experience.

[A list of compatibility options can be found here](/Usage/Settings-Compatibility.md).