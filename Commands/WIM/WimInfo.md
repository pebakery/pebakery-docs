# WimInfo

Retrieves information about a Windows Imaging (.wim) file.

## Syntax

```pebakery
WimInfo,<SrcWim>,<ImageIndex>,<Property>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| SrcWim | The full path to the source files to be captured. |
| ImageIndex | The index of the image within the .wim file to retrieve info from. |
|| 0 - Retrieve basic information about the WIM file. See **WIM File Properties**. |
|| 1 - Retrieve information about the 1st image in the WIM file. |
|| _n_ - Retrieve information about the _nth_ image in the WIM file. |
| Property | The property to query from the image's XML data. Use the `/` character to access nested properties. Multiple nested properties can be accessed by using brackets. (Ex. _WINDOWS/LANGUAGES/LANGUAGE[2]_ indicates the second _LANGUAGE_ element nested within the _WINDOWS/LANGUAGES_ element.) |
| DestVar | The variable where the value of the specified `Property` will be stored. |

### WIM File Properties

The following properties can be retrieved from the WIM file's Header.

| Property | Description |
| --- | --- |
| ImageCount | Returns the number of images the WIM file contains. |
| BootIndex | Returns the index of the bootable image in the .wim file. If there are no bootable images available the value will be zero. |
| Compression | Returns the compression used by the WIM file. `NONE` `XPRESS` `LZX` `LZMS`. |

### Image File Properties

The following image specific properties can be retrieved from the XML data if they are defined.

**Default Image Properties:**

| Property | Description |
| --- | --- |
| DIRCOUNT | Number of directories in the image. |
| FILECOUNT | Number of files in the image.  |
| TOTALBYTES | Amount of space the image will occupy when extracted. |
| HARDLINKBYTES | Additional space the image will require when extracted without using hardlinks. |
| CREATIONTIME | Contains 2 properties: `HIGHTPART` and `LOWPART` that when combined as a 64bit integer represent a Windows timestamp. |
| CREATIONTIME/HIGHPART | Creation Date (Hex) |
| CREATIONTIME/LOWPART | Creation Time (Hex) |
| LASTMODIFICATIONTIME | Contains 2 properties: `HIGHTPART` and `LOWPART` that when combined as a 64bit integer represent a Windows timestamp. |
| LASTMODIFICATIONTIME/HIGHPART | Modified Date (Hex) |
| LASTMODIFICATIONTIME/LOWPART | Modified Time (Hex) |
| NAME | **(User Defined)** Image Name. |
| DESCRIPTION | **(User Defined)** Image Description.  |
| FLAGS | **(User Defined)** Image Flags. |

The WIM file's XML data may also contain arbitrary properties defined by the WIM files author.
The following is a non-exhaustive list of custom image properties present in Windows sources.

**Custom Image Properties:**

| Attribute | Description |
| --- | --- |
| DISPLAY NAME | "Friendly" name used by the Windows installer. |
| DISPLAYDESCRIPTION | "Friendly" description used by the Windows installer. |
| INSTALLATIONTYPE | Install type (Client/Server/Windows PE). |
| WINDOWS/VERSION/BUILD | OS Build Number. |
| WINDOWS/VERSION/MAJOR | OS Major Version. |
| WINDOWS/VERSION/MINOR | OS Minor Version. |
| WINDOWS/VERSION/SPBUILD | OS Service Pack Build Number. |
| WINDOWS/VERSION/SPLEVEL | OS Service Pack Level. |
| WINDOWS/LANGUAGES/DEFAULT | OS Default Language  |
| WINDOWS/EDITIONID | OS Edition (Home/Professional) |

## Remarks

Split WIMs: PEBakery does not support retrieving info from split WIM files (.swm).

This command uses the the open source [Windows Imaging library (wimlib)](https://wimlib.net/).

## Related

[WimMount](./WimMount.md), [WimUnmount](./WimUnmount.md), [WimCapture](./WimCapture.md), [WimAppend](./WimAppend.md), [WimApply](./WimApply.md), [WimExtract](./WimExtract.md), [WimExtractList](./WimExtractList.md)

## Examples

### Example 1

This example script will display information about all images in a WIM file.

```pebakery
[Main]
Title=WimInfo Example
Description=Demonstrate retrieve information about a WIM and the images it contains.
Level=5
Version=1
Author=Homes32

[variables]
%wim%=C:\Temp\Win7\SOURCES\INSTALL.WIM

[Process]
// Get the number of images in the wim file.
// Index 0 references WIM file attributes.
WimInfo,%wim%,0,ImageCount,%imgCount%
// Loop through each image and display the information.
LOOP,%ScriptFile%,DisplayInfo,1,%imgCount%

[DisplayInfo]
System,SetLocal
WimInfo,%wim%,#c,WINDOWS/VERSION/MAJOR,%verMaj%
WimInfo,%wim%,#c,WINDOWS/VERSION/MINOR,%verMin%
WimInfo,%wim%,#c,WINDOWS/VERSION/BUILD,%verBld%
WimInfo,%wim%,#c,WINDOWS/VERSION/SPLEVEL,%verSP%
WimInfo,%wim%,#c,WINDOWS/LANGUAGES/LANGUAGE,%lang%
WimInfo,%wim%,#c,NAME,%imgName%
WimInfo,%wim%,#c,DESCRIPTION,%imgDescr%
WimInfo,%wim%,#c,FLAGS,%imgFlags%
WimInfo,%wim%,#c,DISPLAYNAME,%imgDispName%
WimInfo,%wim%,#c,DISPLAYDESCRIPTION,%imgDispDescr%
Message,"Image: #c of %imgCount%#$xVersion: %verMaj%.%verMin% (Build %verBld% Service Pack %verSP%)#$xLanguage: %lang%#$xName: %imgName%#$xDescription: %imgDescr%#$xFlags: %imgFlags%#$xDisplay Name: %imgDispName%#$xDisplay Description: %imgDispDescr%"
System,EndLocal
```
