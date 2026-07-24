# XMLAdd

Add a new element/text/attribute to an XML file.

To update an existing element/attribute you must use the XMLUpdate command.

## Syntax

```pebakery
XMLAdd,<Operation>,<XMLFile>,<XPath>,<Type>,<Name>[,<Value>]
```

### Arguments

| Argument | Description |
| --- | --- |
| Operation |  One of the following: |
| | `Insert`  - Insert a node at the the beginning of the `XPath`. |
| | `Append`  - Append a node to the end of the `XPath`. |
| | `Subnode` - Add a new subnode to each `XPath` in the document. |
| XMLFile | Full path to the .xml filed to edit. |
| XPath | XPath (XML Path Language) query used to insert the Attribute/Element. |
| Type | XPath type: |
|| `Attribute` or `attr` - Attribute
|| `Element` or `elem` - Element
|| `Text` - Text
| Name | Value Name. |
| Value | **(Optional)** The value to add.|

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

[XMLDelete](./XMLDelete.md), [XMLRename](./XMLRename.md), [XMLUpdate](./XMLUpdate.md)

## Examples

### Example 1 - Basic Use

```pebakery

// Add a Subnode called GUIConfig under GUIConfigs
XMLAdd,SubNode,%config.xml%,"NotepadPlus/GUIConfigs","Element","GUIConfig",""

// Insert a new attribute into an XML file.
XMLAdd,Insert,%config.xml%,"NotepadPlus/GUIConfigs/GUIConfig[not(@name)]","Attribute","name","DarkMode"

// Append an attribute to the DarkMode attribute
XMLAdd,Append,%config.xml%,"NotepadPlus/GUIConfigs/GUIConfig[@name='DarkMode']","Attribute","enable","yes"

```

### Example 2 - Working with Default Namespaces

When an XML file declares a default namespace (without a prefix), PEBakery exposes it using the `_` prefix in XPath queries and attribute names.

#### XML File

```xml
<?xml version="1.0" encoding="UTF-8"?>
<NotepadPlus xmlns="http://notepad-plus-plus.org/ns">
  <GUIConfigs>
    <GUIConfig name="ExistingConfig">true</GUIConfig>
  </GUIConfigs>
</NotepadPlus>
```

#### Commands

```pebakery
// Add a new GUIConfig subnode under GUIConfigs
XMLAdd,SubNode,%config.xml%,"_:NotepadPlus/_:GUIConfigs","elem","GUIConfig",""

// Insert a name attribute into the new GUIConfig element
XMLAdd,Insert,%config.xml%,"_:NotepadPlus/_:GUIConfigs/_:GUIConfig[not(@name)]","attr","name","DarkMode"

// Append an enable attribute to the DarkMode GUIConfig
XMLAdd,Append,%config.xml%,"_:NotepadPlus/_:GUIConfigs/_:GUIConfig[@name='DarkMode']","attr","enable","yes"
```

### Example 3 - Working with Namespaced XML

When working with XML files that use namespace prefixes, use the prefix defined in the file's namespace declarations in your XPath and attribute names.

#### XML File

```xml
<?xml version="1.0" encoding="UTF-8"?>
<oor:items xmlns:oor="http://openoffice.org/2001/registry"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <item oor:path="/org.openoffice.Office.Common/Help">
    <prop oor:name="ExtendedTip" oor:op="fuse">
      <value>false</value>
    </prop>
  </item>
</oor:items>
```

#### Commands

```pebakery
// Append a new <item> element to the root
XMLAdd,Append,%registrymodifications.xcu%,"oor:items","Element","item",""

// Set the namespaced oor:path attribute on the new item
XMLAdd,Append,%registrymodifications.xcu%,"oor:items/item[last()]","Attribute","oor:path","/org.openoffice.Office.Common/Misc"

// Add a namespaced <prop> child element with attributes
XMLAdd,Append,%registrymodifications.xcu%,"oor:items/item[last()]","Element","prop",""
XMLAdd,Append,%registrymodifications.xcu%,"oor:items/item[last()]/prop","Attribute","oor:name","FirstRun"
XMLAdd,Append,%registrymodifications.xcu%,"oor:items/item[last()]/prop","Attribute","oor:op","fuse"

// Add the value element
XMLAdd,Append,%registrymodifications.xcu%,"oor:items/item[last()]/prop","Element","value","false"
```