# WimCapture

Creates a new Windows Imaging (WIM) archive.

**Warning!** This command is unstable and may be changed in a future release.

## Syntax

```pebakery
WimCapture,<SrcDir>,<DestWim>,<Compress>[,IMAGENAME=STR][,IMAGEDESC=STR][,FLAGS=STR][,BOOT][,CHECK][,NOACL]
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
| IMAGENAME= | **(Optional)** The unique name for the image being captured. If not specified it will defaults to the filename component of `SrcWim`. |
| IMAGEDESC= | **(Optional)** Additional information about the image. |
| FLAGS= | **(Optional)** Specify a string to use in the <FLAGS> element of the XML data for the new image. |

The arguments `IMAGENAME=`, `IMAGEDESC=`, and `FLAGS=` can be used independently and can be specified in any order.

### Flags

The following flags can be used independently and can be specified in any order.

| Argument | Description |
| --- | --- |
| BOOT | **(Optional)** Mark the new image as the "bootable" image of the WIM. |
| CHECK | **(Optional)** Include extra integrity information in the resulting WIM.  |
| NOACL | **(Optional)** Do not capture security descriptors on files and directories. |

## Remarks

Data integrity: WIM files include checksums of file data. In addition, a WIM file can include an integrity table (extra checksums) over the raw data of the entire WIM file. For performance reasons wimlib does not create the integrity table by default, but the `CHECK` flag can be specified to make it do so.

This command uses the the open source [Windows Imaging library (wimlib)](https://wimlib.net/).

## Related

[WimUnmount](./WimUnmount.md)

## Examples



### Example 1

```pebakery

```
