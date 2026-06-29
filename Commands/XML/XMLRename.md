# XMLRename

Rename a value in an XML file.

The `XPath` must exist in order for the value to be Renamed.

## Syntax

```pebakery
XMLRename,<XMLFile>,<XPath>,<Value>
```

### Arguments

| Argument | Description |
| --- | --- |
| XMLFile | Full path to the .xml filed to edit. |
| XPath | XPath (XML Path Language) query used to locate the Attribute/Element to rename. |
| Value | New name. |

## Return Codes

None.

## Remarks

If the command fails the build will halt.

Default namespaces are exposed with the `_` prefix.

 - Every element in the XPath must carry the `_:` prefix since they all inherit the default namespace — there's no un-namespaced fallback.
 - Attributes like name and enable don't get the `_:` prefix because attributes don't inherit the default namespace unless explicitly declared.

XML files are output as UTF-8 (no BOM).

For more information about using XPath syntax check out this [XPath Tutorial](https://www.w3schools.com/xml/xpath_intro.asp).

## Related

[[XMLAdd]], [[XMLDelete]], [[XMLUpdate]]

## Examples

### Example 1

```pebakery

// Rename a Subnode called GUIConfig under GUIConfigs
XMLRename,%config.xml%,"NotepadPlus/GUIConfigs","Configs"

```