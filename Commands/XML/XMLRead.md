# XMLRead

Read an XML value.

If the `XPath` has multiple matches only the first match will be returned.

## Syntax

```pebakery
XMLRead,<XMLFile>,<XPath>,<%DestVar%>[,NOERR]
```

### Arguments

| Argument | Description |
| --- | --- |
| XMLFile | Full path to the XML filed to read. |
| XPath | XPath (XML Path Language) query used to locate the value to read. |
| DestVar | Variable where the value of `XPath` will be stored. |
| NOERR | **(Optional)** Don't Halt on errors. (Use if you intend to handle errors yourself).

## Return Codes

| Code | Description |
| --- | --- |
| %^RET% | Returns the of the following:  |
||`0` - Success|
||`1` - XML File missing or invalid.|
||`2` - XPath not found.|

## Remarks

If the `XPath` does not exist the operation will fail and the build will Halt. You can override this behavior by specifying the `NOERR` flag and checking the value of `%^RET%`. If `NOERR` is specified and the `XPath` does not exist `DestVar` will return an empty string.

Default namespaces are exposed with the `_` prefix.

 - Every element in the XPath must carry the `_:` prefix since they all inherit the default namespace — there's no un-namespaced fallback.
 - Attributes like name and enable don't get the `_:` prefix because attributes don't inherit the default namespace unless explicitly declared.

For more information about using XPath syntax check out this [XPath Tutorial](https://www.w3schools.com/xml/xpath_intro.asp).

## Related

[[XMLAdd]], [[XMLCount]], [[XMLDelete]], [[XMLQuery]], [[XMLReadList]], [[XMLRename]], [[XMLUpdate]]

## Examples

### Example 1 - Basic Use

#### XML File

```XML
<configuration>
  <userSettings>
    <App.Properties.Settings>
      <setting name="Theme" serializeAs="String">
        <value>Light</value>
      </setting>
    </App.Properties.Settings>
  </userSettings>
</configuration>
```

#### Commands

```pebakery

XMLRead,"C:\Temp\Test.xml","/configuration/userSettings/App.Properties.Settings/setting[@name='Theme']/value",%Value%
// Returns "Light"
Message,"[%Value%]"

```

### Example 2 - Working with Default Namespaces

When an XML file declares a default namespace (without a prefix), PEBakery exposes it using the `_` prefix in XPath queries and attribute names.

#### XML File

```XML
<wlan xmlns="urn:test">
	<SSIDConfig>
		<SSID>
			<name>WiFi</name>
		</SSID>
	</SSIDConfig>
	<items>
		<item>A</item>
		<item>B</item>
	</items>
</wlan>
```

#### Commands

```pebakery

XMLRead,"C:\Temp\Test.xml","//_:SSIDConfig/_:SSID/_:name/text()",%Value%,NOERR
// Returns "WiFi"
Message,"[%Value%]"

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

XMLRead,"C:\Temp\Test.xml","/oor:items/item/prop/value",%Value%
// Returns "false"
Message,"[%Value%]"

```