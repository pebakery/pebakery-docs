# Exit

Stop running a section immediately and return to the calling script/section.

## Syntax

```pebakery
Return,[VALUE]
```

### Arguments

| Argument | Description |
| --- | --- |
| Return Value | **(Optional)** Will set value of the `#r` token, which will be made available to the caller upon return. |

## Remarks

Calling `Return` directly from the `[Process]` section of the calling script has the same effect as the `Exit,NOWARN` command, and will abort the running script.

## Related

[Run](../Branch/Run.md)

## Examples

### Example 1

Stop processing the current section and return.

```pebakery
Set,%var%,2
If,Not,%var%,Equal,1,Return
Echo,"We should never get here..."
```

### Example 2

Stop processing the current section and return, setting the value of `#r` to `%var%`.

```pebakery
Set,%var%,2
If,Not,%var%,Equal,1,Return,%var%
Echo,"We should never get here..."
```