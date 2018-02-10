# Script Levels

Levels are used by PEBakery to determine the correct grouping and sequence in which scripts will be processed.

## Processing Order

PEBakery will use the following properties to determine the processing order of a script:

1. Script Level
1. Folder Name
1. File Name

### Levels

There are 10 levels defined by PEBakery. Processing starts at level 1 and continues on to the subsequent level after all scripts under the current level are processed.

Scripts with negative levels will be hidden from the project tree and will not be processed. These scripts are intended to be used as a library to store configuration, macros, code, or attached files used by other scripts when such items do not need to be directly accessed by the end user.

The following table shows the various script levels and their recommended use. Strict adherence to this policy is not enforced by PEBakery, but is strongly encouraged in order to maximize interoperability between projects.

| Level | Usage | Description |
| ---: | --- | --- |
| 1<br/>-1 | Pre-Process | Project options, Configure source files, Mounting/Extracting WIMs, etc.  |
| 2<br/>-2 | Build | Create folders, Copy/Expand/Extract files, Registry hives, WOW64, etc. |
| 3<br/>-3 | Shell & Components | Shell, Ramdisk/FBWF, Networking, Optional components (Bitlocker, Search, .Net/VC++ Runtime, etc.) |
| 4<br/>-4 | Settings/Tweaks | Settings such as wallpaper, theme, power options, computer name, system local, etc. |
| 5<br/>-5 | Applications | Programs and tools to be used in the PE environment. |
| 6<br/>-6 | Drivers | Additional drivers needed. (Chipset/LAN/SATA/RAID/VGA/WLAN) |
| 7<br/>-7 | OtherOS | Bootable OS images to be added to the target. Typically used to include pre-built bootable images such as chntpw, Hirens, Memtest86+, PartedMagic, UBCD, etc. that can be loaded using a boot manager such as grub4dos or syslinux. |
| 8<br/>-8 | Post-Processing | Creating shortcuts, Capture WIMs, Cleanup, etc. |
| 9<br/>-9 | Emulation & Media Creation | Create/Burn ISO, Copy to USB, Test with Qemu/vmWare/VirtualPC |
| 10<br/>-10 | Project Tools | Additional tools for working with a project but usually not part of the build process. (WIM manipulation, Hive editing, Target tweaking, etc.) 

### Folder Names

Folders and Sub-folders can be used to organize and group scripts within the same level. Folders are processed in alpha numeric order and the folder name is displayed in the project tree.

Folders may be duplicated in the project tree if script files with different levels reside within the same folder.

### File Names

Script files within their corresponding folder are processed in alpha numeric order according to their filename.

## Remarks

None.