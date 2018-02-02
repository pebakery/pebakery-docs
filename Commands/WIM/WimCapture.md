# WimCapture

Creates a new Windows Imaging File (.WIM).

## Syntax

```pebakery
WimCapture,<SrcDir>,<DestWim>,<Compress>[,ImageName=<String>][,ImageDesc=<String>][,Flags=<String>][,BOOT][,CHECK][,NOACL]
```

### Arguments

| Argument | Description |
| --- | --- |
| SrcWim | The full path to the source files to be captured. |
| DestWim | The full path to the .wim file being created. If the file exists it will be overwritten. If the directory structure does not exist it will be created. |
| Compress | Supported Compression levels: |
|| NONE - No Compression. |
|| XPRESS - Fast compression and decompression, but results in a larger image size. _(Similar to DISM.exe  /compress:fast )_ |
|| LZX - Zip style DEFLATE compression. _(Similar to DISM.exe: /compress:maximum)_ |
|| LZMS - Microsoft's undocumented compression format similar to the LZMA algorithm used by 7zip. Smaller image size, but takes significantly longer to compress. _(Similar to DISM.exe /compress:recovery)_ |
| ImageName= | **(Optional)** The unique name for the image being captured. If not specified it will default to the filename component of `SrcWim`. |
| ImageDesc= | **(Optional)** Additional information about the image. |
| Flags= | **(Optional)** Specify a string to use in the `<FLAGS>` element of the XML data for the new image. |

The arguments `ImageName=`, `ImageDesc=`, and `Flags=` can be used independently and can be specified in any order.

### Flags

The following flags can be used independently and can be specified in any order.

| Argument | Description |
| --- | --- |
| BOOT | **(Optional)** Mark the new image as the "bootable" image of the WIM file. |
| CHECK | **(Optional)** Include extra integrity information in the resulting WIM file.  |
| NOACL | **(Optional)** Do not capture security descriptors on files and directories. |

## Remarks

Data integrity: WIM files include checksums of all file data. In addition, a WIM file can include an integrity table (extra checksums) over the raw data of the entire WIM file. For performance reasons PEBakery does not create the integrity table by default, but the `CHECK` flag can be specified to make it do so.

This command uses the the open source [Windows Imaging library (wimlib)](https://wimlib.net/).

## Related

[WimMount](./WimMount.md), [WimUnmount](./WimUnmount.md), [WimAppend](./WimAppend.md)

## Examples

### Example 1

Create a bootable .wim archive using _LZX_ compression from _C:\Temp\Target_

```pebakery
WimCapture,C:\Temp\Target,C:\Temp\Target\TEST.WIM,LZX,ImageName="MyBootImage",BOOT
```