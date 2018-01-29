# WimApply

Extracts ("applies") an image, or all images, from a Windows Imaging (WIM) archive.

## Syntax

```pebakery
WimApply,<SrcWim>,<ImageIndex>,<DestDir>[,CHECK][,NOACL][,NOATTRIB]
```

### Arguments

| Argument | Description |
| --- | --- |
| SrcWim | The full path to the .wim file that to be mounted. |
| ImageIndex | The index of the image in the .wim file to be applied. |
| DestDir | The full path to the directory where the .wim file is to be applied. If the directory does not exist or there is already an image mounted the operation will fail. |

### Flags

The following flags can be used independently and can be specified in any order.

| Argument | Description |
| --- | --- |
| CHECK | **(Optional)** Verify the integrity of `SrcWim` if it contains extra integrity information. |
| NOACL | **(Optional)** Do not restore security descriptors on extracted files and directories. |
| NOATTRIB | **(Optional)** Do not restore Windows file attributes such as read-only, hidden, etc. |

## Remarks

Note that WimApply is designed to extract, or "apply", full WIM images. If you want to extract only certain files or directories from a WIM image, use the `WimExtract` command instead.

Data integrity: WIM files include checksums of file data. To detect accidental (non-malicious) data corruption, wimlib calculates the checksum of every file it extracts and issues an error if it does not have the expected value. (This default behavior seems equivalent to the /verify option of ImageX.) In addition, a WIM file can include an integrity table (extra checksums) over the raw data of the entire WIM file. For performance reasons wimlib does not check the integrity table by default, but the `CHECK` flag can be specified to make it do so.

ESD files: wimlib can extract files from solid-compressed WIMs, or "ESD" (.esd) files, just like from normal WIM (.wim) files. However, Microsoft sometimes distributes ESD files with encrypted segments; wimlib cannot extract such files until they are first decrypted.

This command internally uses `wimlib-15.dll`.

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
// Mount the image with index 4
WimMount,%InstallWim%,%WimIndex%,%MountDir%
Echo,"This is where you would copy some files, etc..."
Wait,10
// Cleanup after ourselves...
Echo,"UnMounting %MountDir%..."
WimUnmount,%MountDir%
```
