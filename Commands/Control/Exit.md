# Exit

Forces the current script to terminate and continues processing with the next script.

## Syntax

```pebakery
Exit,<Message>[,NOWARN]
```

### Arguments

| Argument | Description |
| --- | --- |
| Message | Text that will be displayed and written to the log citing the reason for the `Exit`. |

### Flags

| Flag | Description |
| --- | --- |
| NOWARN | **(Optional)** Suppresses the Warning state in the log. |

## Remarks

Default behavior is to log the `Exit` action as a warning. If this is not a critical event you can override this behavior with the `NOWARN` flag.

If the script has defined the `System,OnScriptExit` directive the command will be processed before the script exits. This allows the developer to perform further logging and cleanup based on the reason for the `Exit`.

## Related

[System,OnScriptExit](../System/OnScriptExit.md)

## Examples

### Example 1

Stop processing the current script and log a warning.

```pebakery
Exit,"Unable to continue because the file was not found."
```

### Example 2

Stop processing the current script, but don't log a warning.

```pebakery
// No need to warn the user as the action is intended to prevent further processing.
Exit,"The application is already configured.",NOWARN
```