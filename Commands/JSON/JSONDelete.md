# JSONDelete

Delete a value from a JSON file.

## Syntax

```pebakery
JSONDelete,<JSONFile>,<Path>
```

### Arguments

| Argument | Description |
| --- | --- |
| JSONFile | Full path to the JSON value to delete. |
| Path | Path notation used to locate the value to delete. |

## Return Codes

None.

## Remarks

Additional Info: [Supported JSON addressing schemes](./README.md#json-path-notation)

When using JSONPath the path/value will only be deleted when it matches exactly one existing node.

Deleting a `Path` from a file that supports JSONC (JSON with comments) will automatically remove all comments and trailing commas and standardize the file to RFC 8259 compliant JSON.

## Related

[JSONRead](./JSONRead.md), [JSONQuery](./JSONQuery.md), [JSONWrite](./JSONWrite.md)

## Examples

### Example 1

GJSON Style Path

```pebakery

JSONDelete,"C:\Temp\Test.json","JS_FILEEXPLORER.4th_filename"

```

### Example 1

JSONPath

```pebakery

JSONDelete,"C:\Temp\Test.json","$.JS_FILEEXPLORER.4th_filename"

```