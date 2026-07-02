# JSONCount

Perform a count operation on a specific node within a JSON file. 

This allows you to determine how many items are contained in a JSON object or array at a given location (`Path`).

## Syntax

```pebakery
JSONCount,<JSONFile>,<Path>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| JSONFile | Full path to the JSON filed to validate. |
| Path | GJSON or JSONPath notation used to locate the node. |
| DestVar | Variable where the count will be stored. |

## Return Codes

Once the node is found, the count stored in `DestVar` is determined based on the node's type:

| Type | Description |
| --- | --- |
| JsonObject | Returns the number of properties (key-value pairs) in the object. |
| JsonArray | Returns the number of elements in the array. |
| Other (Primitive types like string, number, etc.) | Returns `1` (counting the single value as one item). |
| null | Returns `-1` indicating the path was not found. |
	
## Remarks

JSONCount requires the `Path` to resolve to one effective node.

Additional Info: [Supported JSON addressing schemes](./README.md#JSON Path Notation)

## Related

[JSONQuery](./JSONQuery.md), [JSONRead](./JSONRead.md), [JSONReadArray](./JSONReadArray.md), [JSONReadKeys](./JSONReadKeys.md), [JSONType](./JSONType.md)

## Examples

### JSON File

```JSON
{
    "Name": "App",
    "Items": [
        1,
        "two",
        true
    ],
    "Obj": {
        "B": 2,
        "A": 1
    }
}
```

### Example 1

```pebakery

JSONCount,"C:\Temp\Test.json","Items",%Count%
// Returns "3"
Message,"[%Count%]"

```

### Example 2

```pebakery

JSONCount,"C:\Temp\Test.json","Homes32",%Count%
// Returns "-1" for no path found
Message,"[%Count%]"

```