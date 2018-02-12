# WimPathRename

Move or Rename a file or directory tree in a Windows Imaging (.wim) file.

## Syntax

```pebakery
WimPathRename,<WimFile>,<ImageIndex>,<SrcPath>,<DestPath>[,CHECK][,REBUILD]
```

### Arguments

| Argument | Description |
| --- | --- |
| WimFile | The full path of the .wim file to modify. |
| ImageIndex | The index of the image within the .wim file where the file or directory resides. |
| SrcPath |  The full path of the file or directory to rename. All paths are relative to the image's root directory. If `SrcPath` does not exist the operation will fail. |
| DestPath | The full path to the new location of the file or directory within the WIM file. All paths are relative to the image's root directory. Any existing files or directories will be overwritten. If the directory structure does not exist it will be created. |

### Flags

The following flags can be used independently and can be specified in any order.

| Argument | Description |
| --- | --- |
| CHECK | **(Optional)** Before updating `WimFile`, verify it's integrity if it contains extra integrity information. Also include extra integrity information in the updated WIM even if it was not present before. |
| REBUILD | **(Optional)** Rebuild the entire WIM instead of appending the data to the end of the image. Rebuilding the WIM is slower, but will recover space that would otherwise be left as a hole in the WIM file. |

## Remarks

**Data integrity:** In order to detect accidental (non-malicious) data corruption, the checksum of every file extracted is calculated and an error is returned if it does not match the checksum included in the WIM file. In addition, a WIM file can include an integrity table (extra checksums) over the raw data of the entire WIM file. For performance reasons PEBakery does not verify or create the integrity table by default, but the `CHECK` flag can be specified to make it do so.

This command uses the the open source [Windows Imaging library (wimlib)](https://wimlib.net/).

## Related

[WimMount](./WimMount.md), [WimUnmount](./WimUnmount.md), [WimPathAdd](./WimPathAdd.md), [WimPathDelete](./WimPathDelete.md)

## Examples

### Example 1

This example renames a single file in the 1st image of *C:\Temp\boot.wim*.

```pebakery
Echo,"Rename File..."
WimPathRename,C:\Temp\boot.wim,1,Windows\regedit.exe,Windows\regedit2.exe
```

### Example 2

This example will move the */Program Files/myApp* directory in the 1st image of *C:\Temp\boot.wim* to /Programs/myApp.

```pebakery
Echo,"Moving Directory..."
WimPathRename,C:\Temp\boot.wim,1,"/Program Files/myApp","/Programs/myApp"
```
