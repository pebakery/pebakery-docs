# WimInfo

Retrieves information about a Windows Imaging (.wim) file.

## Syntax

```pebakery
WimInfo,<WimFile>,<ImageIndex>,<Property>,<%DestVar%>[,NOERR]
```

### Arguments

| Argument | Description |
| --- | --- |
| WimFile | The full path to the .wim file. |
| ImageIndex | The index of the image within the WIM file to retrieve info from. |
|| 0 - Retrieve basic information about the WIM file. See **WIM File Properties**. |
|| 1 - Retrieve information about the 1st image in the WIM file. See **Image Properties**. |
|| _n_ - Retrieve information about the _nth_ image in the WIM file. |
| Property | The property to query from the image's XML data. Use the `/` character to access nested properties. Multiple nested properties can be accessed by using brackets. (Ex. _WINDOWS/LANGUAGES/LANGUAGE[2]_ indicates the second _LANGUAGE_ element nested within the _WINDOWS/LANGUAGES_ element.) |
| DestVar | The variable where the value of the specified `Property` will be stored. |

### Flags

The following flags can be used independently and can be specified in any order.

| Argument | Description |
| --- | --- |
| NOERR | **(Optional)** Do not fail if a property does not exist in the `SrcWim` XML data. |

### WIM File Properties

The following properties can be retrieved from the WIM file's Header.

| Property | Description |
| --- | --- |
| ImageCount | The number of images the WIM file contains. |
| BootIndex | The index of the bootable image in the .wim file. If there are no bootable images available the value will be zero. |
| Compression | The compression format used by the WIM file. `NONE` `XPRESS` `LZX` `LZMS`. |

### Image Properties

Individual properties for each image are stored as XML data within the .wim file. These properties include basic information such as the Image Name, Image Description, Size, File/Dir Count, and Created/Modified timestamps. The XML format also allows for additional properties to be defined for each image. Often times this is used by the author to include information that may be used to make a decision on which image should be selected, such as the product version, language, edition, and processor architecture.

#### Default Image Properties

The following image specific properties can be retrieved:

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
| NAME | User defined image name. |
| DESCRIPTION | User defined image description.  |
| FLAGS | User defined image flags. |

#### Additional Image Properties

The WIM file's XML data may also contain arbitrary properties defined by it's author.
The following is a non-exhaustive list of custom image properties used by the Microsoft Windows Operating System sources.

| Property | Description |
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

**Split WIMs:** PEBakery does not support retrieving info from split WIM files (.swm).

This command uses the the open source [Windows Imaging library (wimlib)](https://wimlib.net/).

## Related

[WimMount](./WimMount.md), [WimUnmount](./WimUnmount.md), [WimCapture](./WimCapture.md), [WimAppend](./WimAppend.md), [WimApply](./WimApply.md), [WimExtract](./WimExtract.md), [WimExtractBulk](./WimExtractBulk.md)

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
