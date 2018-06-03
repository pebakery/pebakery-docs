# AddVariables

Reads variables from another section, script, or file into the current scripts run-time environment.

## Syntax

```pebakery
AddVariables,<FileName>,<Section>,[GLOBAL]
```

### Arguments

| Argument | Description |
| --- | --- |
| FileName | The full path of the file to read. **Hint:** Use `%ScriptFile%` to reference the current script.|
| Section | The section containing the variables to be added. |

### Flags

| Flag | Description |
| --- | --- |
| GLOBAL | **(Optional)** The variables are added to the global scope and available to the entire project for the duration of the build. If the variables exist they will be overwritten! |

## Remarks

When a script runs, it automatically adds variables defined in the `[Variables]` section of the script. The `AddVariables` command gives you the flexibility to add additional variables stored in other scripts and files and can be used in *script.project* to load variables and macros for the entire project.

## Related
[Set](./Set.md), [SetMacro](./SetMacro.md)

## Examples

### Example 1

```pebakery
// Add variables from another section in the current script
AddVariables,%ScriptFile%,AlternativeVariables
```

### Example 2

The following code if placed in *script.project* will load macros defined in a script "library" for use by the entire project.

```pebakery
// Add macros from another script so they are available to all scripts
AddVariables,%BaseDir%\Build\Library.script,ApiVar,GLOBAL
```
