# JSONType

Identify the data type of a specific element within a JSON file.

## Syntax

```pebakery
JSONType,<JSONFile>,<Path>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| JSONFile | Full path to the JSON filed to validate. |
| Path | GJSON or JSONPath notation used to locate the node. |
| DestVar | Variable where the data type will be stored. |

## Return Codes

Once the node is found, the value stored in `DestVar` is determined based on the node's type:

| Type | Return Value |
| --- | --- |
| JsonObject | `Object` |
| JsonArray |  `Array` |
| String | `String` |
| Number | `Number` |
| True/False | `Boolean` |
| null | Returns `Missing` indicating the path was not found. |
	
## Remarks

JSONType requires the `Path` to resolve to one effective node.

Additional Info: [Supported JSON addressing schemes](./README.md#JSON Path Notation)

## Related

[JSONCount](./JSONCount.md), [JSONQuery](./JSONQuery.md), [JSONRead](./JSONRead.md), [JSONReadArray](./JSONReadArray.md), [JSONReadKeys](./JSONReadKeys.md)

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

JSONType,"C:\Temp\Test.json","Items",%Type%
// Returns "Array"
Message,"[%Type%]"

```

### Example 2

```pebakery

JSONType,"C:\Temp\Test.json","Obj",%Type%
// Returns "Object"
Message,"[%Type%]"

```

### Example 3

```pebakery

JSONType,"C:\Temp\Test.json","Homes32",%Count%
// Returns "Missing" for no path found
Message,"[%Count%]"

```