# PEBakery Utilities

PEBakery Utilities are a collection of tools useful for project and script developers.

## Codebox

Codebox is a disposable script processor that can be used to quickly test commands and code snippets in the context of a specific project. Each CodeBox script runs under the exact same conditions as any other script inside your selected project, making this a good tool for debugging variables and commands.

The contents of the CodeBox are stored in `CodeBox.txt`, which is located in the base directory (`%BaseDir%`) of your project.

At minimum each CodeBox must contain a `[Process]` section.

## String Escaper

The String Escaper tool allows you to quickly escape or unescape special characters in a string.

For more information on escape characters please refer to the [Script Syntax](../LangRef/Syntax.md) documentation.

## Syntax Checker

The Syntax Checker validates code snippets to ensure they will run correctly in PEBakery.