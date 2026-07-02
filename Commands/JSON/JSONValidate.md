# JSONValidate

Verify the integrity and structure of a JSON file.

## Syntax

```pebakery
JSONValidate,<JSONFile>,<%DestVar%>[,STRICT][,NOERR]
```

### Arguments

| Argument | Description |
| --- | --- |
| JSONFile | Full path to the JSON filed to validate. |
| DestVar | Variable where the result of the validation will be stored. |
| Strict | **(Optional)** If `Strict` flag is specified, the JSON file must be strictly RFC 8259 compliant. If omitted, the default behavior permits the presence of JSONC extensions, such as comments. |
| NOERR | **(Optional)** Don't Halt if validation fails. (Use if you intend to handle errors yourself).

## Return Codes

| Variable | Description |
| --- | --- |
| DestVar | Returns the of the following:  |
|| `True` - The JSON file is valid. |
|| `False` - The JSON file is not valid. |

## Remarks

JSONValidate ensures a JSON file is "Well-Formed" but it does not validate that it conforms to a specific data model or schema.
 
## Related

[JSONCount](./JSONCount.md), [JSONDelete](./JSONDelete.md), [JSONQuery](./JSONQuery.md), [JSONRead](./JSONRead.md), [JSONReadArray](./JSONReadArray.md), [JSONReadKeys](./JSONReadKeys.md), [JSONType](./JSONType.md), [JSONWrite](./JSONWrite.md)

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

JSONValidate,"C:\Temp\Test.json",%isValid%
// Returns "True" for a valid JSON file.
Message,"[%isValid%]"

```