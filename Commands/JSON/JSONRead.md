# JSONRead

Read a value from a JSON file.

If the `Path` has multiple matches only the first match will be returned.

## Syntax

```pebakery
JSONRead,<JSONFile>,<Path>,<%DestVar%>[,NOERR]
```

### Arguments

| Argument | Description |
| --- | --- |
| JSONFile | Full path to the JSON filed to read. |
| Path | GJSON or JSONPath notation used to locate the value to read. |
| DestVar | Variable where the value of `Path` will be stored. |
| NOERR | (Optional) Don't Halt on errors. (Use if you intend to handle errors yourself).

## Return Codes

| Code | Description |
| --- | --- |
| %^RET% | Returns the of the following:  |
||`0` - Success|
||`1` - JSON file missing or invalid.|
||`2` - Path not found.|

## Remarks

JSONRead requires the `Path` to resolve to one effective node.

If your `Path` resolves to a node that is not a simple field value (bool/number/string), `DestVar` will return a serialized JSON blob containing the entire object or array.

Additional Info: [Supported JSON addressing schemes](./README.md#JSON Path Notation)

## Related

[JSONCount](./JSONCount.md), [JSONQuery](./JSONQuery.md), [JSONReadArray](./JSONReadArray.md), [JSONReadKeys](./JSONReadKeys.md), [JSONType](./JSONType.md)

## Examples

### JSON File

```JSON
{
    "JS_TASKBAR": {
        "theme": "light"
    },
    "Microsoft.PowerShell:ExecutionPolicy": "RemoteSigned",
    "Items": [
        1,
        "two"
    ]
}
```

### Example 1

```pebakery

JSONRead,"C:\Temp\Test.json","JS_TASKBAR.theme",%Value%
// Returns "light"
Message,Return [%Value%]

```

### Example 2

```pebakery

JSONRead,"C:\Temp\Test.json","JS_TASKBAR.theme2",%Value%,NOERR
If,Not,%^RET%,Equal,0,Set,%Value%,"dark"
// Returns "dark"
Message,Return [%Value%]

```