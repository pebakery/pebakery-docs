# XMLUpdate

Update the value of an existing Attribute/Element.

The `XPath` must exist in order for the value to be updated.

## Syntax

```pebakery
XMLUpdate,<XMLFile>,<XPath>,<Value>,[NOERR]
```

### Arguments

| Argument | Description |
| --- | --- |
| XMLFile | Full path to the .xml filed to edit. |
| XPath | XPath (XML Path Language) query used to locate the Attribute/Element to update. |
| Value | New Value. |
| NOERR | NOERR - Don't Halt on errors. (Use if you intend to handle errors yourself). |

## Return Codes

| Variable | Description |
| --- | --- |
| %^RET% | Returns of the the following: |
| | `0` - Success |
| | `1` - Missing or Invalid XML File |
| | `2` - XPath does not exist |

## Remarks

If the command fails the build will halt unless the `NOERR` parameter is specified.

Default namespaces are exposed with the `_` prefix.

 - Every element in the XPath must carry the `_:` prefix since they all inherit the default namespace — there's no un-namespaced fallback.
 - Attributes like name and enable don't get the `_:` prefix because attributes don't inherit the default namespace unless explicitly declared.

XML files are output as UTF-8 (no BOM).

For more information about using XPath syntax check out this [XPath Tutorial](https://www.w3schools.com/xml/xpath_intro.asp).

## Related

[[XMLAdd]], [[XMLDelete]], [[XMLRename]]

## Examples

### Example 1

```pebakery

XMLUpdate,%config.xml%,"NotepadPlus/GUIConfigs/GUIConfig[@name='stylerTheme']/@path","X:\Users\Default\AppData\Roaming\Notepad++\themes\DarkModeDefault.xml",NOERR
If,%^RET%,Equal,2,Begin
  // Node <GUIConfig name='DarkMode'> does not exist, we need to create it
  XMLAdd,SubNode,%config.xml%,"NotepadPlus/GUIConfigs","elem","GUIConfig",""
  XMLAdd,Insert,%config.xml%,"NotepadPlus/GUIConfigs/GUIConfig[not(@name)]","attr","name","stylerTheme"
  XMLAdd,Append,%config.xml%,"NotepadPlus/GUIConfigs/GUIConfig[@name='stylerTheme']","attr","path","X:\Users\Default\AppData\Roaming\Notepad++\themes\DarkModeDefault.xml"
End

```