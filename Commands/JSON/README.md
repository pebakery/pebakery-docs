# JSON (JavaScript Object Notation) Commands

Commands for working with JSON files.

Click on a Command name for a detailed description.

| Command | Description |
| --- | --- |
| [JSONCount](./JSONCount.md) | Perform a count operation on a specific node within a JSON file.  |
| [JSONDelete](./JSONDelete.md) | Delete values from a JSON file. |
| [JSONFormat](./JSONFormat.md) | Format and indent a JSON file for easy human reading or compact it for smaller size. |
| [JSONQuery](./JSONQuery.md) | Read values from a JSON file. |
| [JSONRead](./JSONRead.md) | Read a value from a JSON file. |
| [JSONReadArray](./JSONReadArray.md) | Extract all elements from an array within a JSON file and return them as a delimited string. |
| [JSONReadKeys](./JSONReadKeys.md) | Extract all the property names (keys) from a specific JsonObject within a JSON file and return them as a delimited string. |
| [JSONType](./JSONType.md) | Identify the data type of a specific element within a JSON file. |
| [JSONValidate](./JSONValidate.md) | Verify the integrity and structure of an JSON file. |
| [JSONWrite](./JSONWrite.md) | Add/Modify values in a JSON value. |

## JSON Path Notation

PEBakery supports JSON data manipulation using three distinct addressing schemes. Choose your scheme based on the operation (Read vs. Write/Modify).

| Scheme | Primary Use | Specification |
| --- | --- | --- |
| GJSON | Reading data. | [GJSON Syntax ](https://github.com/tidwall/gjson/blob/master/SYNTAX.md) |
| SJSON | Adding/Modifying data. | [SJSON Syntax](https://github.com/tidwall/sjson#path-syntax) |
| JSONPath | Reading/Modifying data. | [JSONPath](https://www.rfc-editor.org/info/rfc9535/) |

### GJSON/SJSON Scheme

PEBakery utilizes a subset of the GJSON and SJSON formats, commonly found in tools like the [JSON Stream Editor](https://github.com/tidwall/jj).

- Escaping: Use `\` to escape dot `.` or colon `:` characters within keys.
- Root: `.` selects the root document.
- Property Access: Use `.foo` or `foo` for properties; chain them (e.g., .foo.bar) for nested data.
- Array Access: Both `.items[0]` and `.items.0` are supported for compatibility.
- Example: `Microsoft\.PowerShell:ExecutionPolicy` treats the dot as a literal character rather than a path separator.

### JSONPath Scheme:

Paths beginning with the `$` character are processed using the RFC 9535 JSONPath standard.

- `$.JS_TASKBAR.theme`
- `$['Microsoft.PowerShell:ExecutionPolicy']`
- `$.Items[*]`
- `$.Store.Book[?@.Price < 10]`

### Unsupported JSON commands:

The following query languages and features are not supported by PEBakery:

- jq: No support for jq filters or jq-compatible syntax.
- Query Languages: JMESPath and JSONata are not supported.
- Pipelines: Multi-result filter pipelines are unavailable. Use command-specific helpers like `JSONReadArray` or `JSONReadKeys` for complex operations.
