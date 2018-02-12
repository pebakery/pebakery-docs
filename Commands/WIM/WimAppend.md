# WimAppend

Adds an image to an existing Windows Imaging (.wim) file.

## Syntax

```pebakery
WimAppend,<SrcDir>,<DestWim>[,ImageName=<String>][,ImageDesc=<String>][,Flags=<String>][,DeltaIndex=<Integer>][,BOOT][,CHECK][,NOACL]
```

### Arguments

| Argument | Description |
| --- | --- |
| SrcDir | The full path to the source files to be captured. |
| DestWim | The full path to the .wim file being created. If the file exists it will be overwritten. If the directory structure does not exist it will be created. |
| ImageName= | **(Optional)** The unique name for the image being captured. If not specified it will default to the filename component of `SrcWim`. |
| ImageDesc= | **(Optional)** Additional information about the image. |
| Flags= | **(Optional)** Specify a string to use in the `<FLAGS>` element of the XML data for the new image. |
| DeltaIndex= | **(Optional)** An integer representing an existing image inside the `DestWim` archive. Any file data that would ordinarily need to be archived in the new or updated WIM file is omitted if it is already present in the `SrcWim` image on which the delta is being based. The resulting WIM file will still contain a full copy of the image metadata, but this is typically only a small fraction of the WIM file’s total size. |

The arguments `DeltaIndex=`,`ImageName=`, `ImageDesc=`, and `Flags=` can be used independently and can be specified in any order.

### Flags

The following flags can be used independently and can be specified in any order.

| Argument | Description |
| --- | --- |
| BOOT | **(Optional)** Mark the new image as the "bootable" image of the WIM file. |
| CHECK | **(Optional)** Include extra integrity information in the resulting WIM file.  |
| NOACL | **(Optional)** Do not capture security descriptors on files and directories. |

## Remarks

**Data integrity:** WIM files include checksums of all file data. In addition, a WIM file can include an integrity table (extra checksums) over the raw data of the entire WIM file. For performance reasons PEBakery does not create the integrity table by default, but the `CHECK` flag can be specified to make it do so.

**Warning:** It has been observed that wimlib's `--update-of` mode used by the `DeltaIndex` argument is not completely reliable at detecting changes in file contents, sometimes causing the old contents of a few files to be archived rather than the current contents. The cause of this problem is that Windows does not immediately update a file’s last modification time-stamp after every write to that file. Unfortunately, there is no known way for applications like wimlib to automatically work around this bug. Manual workarounds are possible; theoretically, taking any action that causes the problematic files to be closed, such as restarting applications or the computer itself, should cause the file's last modification timestamps to be updated. Also note that wimlib compares file sizes as well as timestamps in determining whether a file has changed, which helps make the problem less likely to occur.

**Split WIMs:** PEBakery does not support appending to split WIM files (.swm).

This command uses the the open source [Windows Imaging library (wimlib)](https://wimlib.net/).

## Related

[WimMount](./WimMount.md), [WimUnmount](./WimUnmount.md), [WimCapture](./WimCapture.md), [WimPathAdd](./WimPathAdd.md), [WimPathDelete](./WimPathDelete.md), [WimPathRename](./WimPathRename.md)

## Examples

### Example 1

Capture data into an existing .wim file.

```pebakery
WimAppend,"C:\Temp\Target","C:\Temp\Target\TEST.WIM"
```
