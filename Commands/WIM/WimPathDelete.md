# WimPathDelete

Removes a file or directory tree from a Windows Imaging (.wim) file.

## Syntax

```pebakery
WimPathDelete,<WimFile>,<ImageIndex>,<Path>[,CHECK][,REBUILD]
```

### Arguments

| Argument | Description |
| --- | --- |
| WimFile | The full path of the .wim file to modify. |
| ImageIndex | The index of the image within the .wim file from which the files will be removed. |
| Path |  The full path of the file or directory to remove from the image. All paths are relative to the image's root directory. If `SrcPath` does not exist the operation will fail.|

### Flags

The following flags can be used independently and can be specified in any order.

| Argument | Description |
| --- | --- |
| CHECK | **(Optional)** Before updating `WimFile`, verify it's integrity if it contains extra integrity information. Also include extra integrity information in the updated WIM even if it was not present before. |
| REBUILD | **(Optional)** Rebuild the entire WIM instead of simply removing the files from the image. Rebuilding the WIM is slower, but will recover space that would otherwise be left as a hole in the WIM file. |

## Remarks

**Data integrity:** In order to detect accidental (non-malicious) data corruption, the checksum of every file extracted is calculated and an error is returned if it does not match the checksum included in the WIM file. In addition, a WIM file can include an integrity table (extra checksums) over the raw data of the entire WIM file. For performance reasons PEBakery does not verify or create the integrity table by default, but the `CHECK` flag can be specified to make it do so.

This command uses the the open source [Windows Imaging library (wimlib)](https://wimlib.net/).

## Related

[WimMount](./WimMount.md), [WimUnmount](./WimUnmount.md), [WimDelete](./WimDelete.md), [WimPathAdd](./WimPathAdd.md), [WimPathRename](./WimPathRename.md)

## Examples

### Example 1

This example removes a single file from the 1st image of *C:\Temp\boot.wim*.

```pebakery
Echo,"Delete File..."
WimPathDelete,C:\Temp\boot.wim,1,Windows\regedit.exe
```

### Example 2

This example will remove the *\Program Files\myApp* directory from the 1st image of *C:\Temp\boot.wim*.

```pebakery
Echo,"Removing Directory..."
WimPathDelete,C:\Temp\boot.wim,1,"/Program Files/myApp"
```
