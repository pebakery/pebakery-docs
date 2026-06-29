# XMLValidate

Verify the integrity and structure of an XML file against either an XML Schema (XSD) or a Document Type Definition (DTD). It can also perform a simple structural validation check.

## Syntax

```pebakery
XMLValidate,<XMLFile>,<%DestVar%>[,Schema=<XsdFile>|Dtd=<DtdFile>|NOERR]
```

### Arguments

| Argument | Description |
| --- | --- |
| XMLFile | Full path to the XML filed to validate. |
| DestVar | Variable where the result of the validation will be stored. |
| Validation Method - **(Optional)** One of the following: |
|| `Schema=` - Validate the file with an XML Schema (XSD) where `XsdFile` is the full path to the schema file. |
|| `Dtd=` - Validate the file with an Document Type Definition (DTD) where `XsdFile` is the full path to the definition file. |
| NOERR | **(Optional)** Don't Halt if validation fails. (Use if you intend to handle errors yourself).

## Return Codes

| Variable | Description |
| --- | --- |
| DestVar | Returns the of the following:  |
|| `True` - The XML file is valid and conforms to the specified Schema/DTD. |
|| `False` - The XML file is not valid and/or does not conform to the specified Schema/DTD. |

## Remarks

You cannot specify both XSD and DTD validation in the same command.

Omitting the Validation Method will parse the `XMLFile` and ensure it is "Well-Formed" but it does not validate that it conforms to a specific data model.

## Related

[XMLAdd]], [XMLDelete]], [[XMLRead]], [[XMLUpdate]]

## Examples

### XML File

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

### Example 1

```pebakery

XMLValidate,"C:\Temp\Test.xml",%isValid%
// Returns True for a valid XML file.
Message,"[%isValid%]"

```

### Example 2

```pebakery

XMLValidate,"C:\Temp\Test.xml",%isValid%,Schema=C:\Temp\Test.xsd
// Returns True if the document structure conforms to the Schema.
Message,"[%isValid%]"

```