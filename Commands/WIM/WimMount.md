# WimMount

Mounts an image in a Windows Imaging File (.WIM) to the specified directory.

Note: Due to the poor performance of Microsoft's mount drivers it is strongly recommended to work with WIM files directly using commands such as `WimAppend`, `WimCapture`, `WimExtract`, `WimPathAdd`, etc. whenever possible.

## Syntax

```pebakery
WimMount,<WimFile>,<Index>,<MountDir>,<MountOption>
```

### Arguments

| Argument | Description |
| --- | --- |
| WimFile | The full path of the .wim file to be mounted. |
| Index | The index of the image in the .wim file to be mounted. |
| MountDir | The full path of the directory where the .wim file is to be mounted. If the directory does not exist or there is already an image mounted the operation will fail. |
| MountOption | Must be one of the following: |
|| READONLY - Mounts the WIM image as read-only. |
|| READWRITE - Mounts the WIM image as writable. |

## Remarks

You must unmount the image using the `WimUnmount` command when you are finished. If you mounted the image as `READWRITE` the image will not be modified unless the `COMMIT` directive is also specified in the `WimUnmount` command.

This command uses the `wimgapi.dll` library included with Microsoft Windows.

## Related

[WimUnmount](./WimUnmount.md)

## Examples

Mount the install.wim image to our *%BaseDir%\Mount\InstallWim* folder.

### Example 1

```pebakery
[Main]
Title=WimMount Example
Description=Show usage of the WimMount command.
Author=Homes32
Level=5
Version=1

[Variables]
%InstallWim%=C:\W10\x64\sources\install.wim
%WimIndex%=4
%MountDir%=C:\PEBakery\Mount\Win10PESE\Source\InstallWimSrc

[Process]
// the directory %MountDir% must exist or the mount operation will fail.
If,Not,EXISTDIR,%MountDir%,DirMake,%MountDir%
Echo,"Mounting Install.wim from#$x--> %InstallWim% [Index: %WimIndex%]"
// Mount the image with index 4 as writable.
WimMount,%InstallWim%,%WimIndex%,%MountDir%,READWRITE
Echo,"This is where you would copy some files, etc..."
Wait,10
// Commit our changes and unmount the image...
Echo,"UnMounting %MountDir%..."
WimUnmount,%MountDir%,COMMIT
```