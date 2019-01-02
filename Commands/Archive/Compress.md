# Compress

Compress a file or directory into an archive.

Wildcards are supported, allowing multiple files to be archived at one time.

## Syntax

```pebakery
Compress,<Format>,<SrcPath>,<DestArchive>,[CompressLevel]
```

### Arguments

| Argument | Description |
| --- | --- |
| Format | Archive format: |
|| `7z` - Use the 7-Zip archive format. (Best Compression) |
|| `Zip` - Use the standard Zip format. (Maximum Portability) |
| SrcPath | Full path of the file(s)/directory to compress. Wildcards (* ?) are allowed.|
| DestArchive | Full path where the archive will be created. If the archive exists the files will be added to the existing archive. |
| CompressLevel | **(Optional)** Supported compression levels: |
|| `Store` -  No compression. Best performance for files that don't benefit from compression. |
|| `Fastest` - Fast compression but results in a larger archive size. |
|| `Normal` - **(Default)** Balance between speed and archive size. |
|| `Best` - Maximum compression results in the smallest archive size at the expense of slower compression/decompression. |

## Remarks

All filenames are encoded to UTF-8.

Compressing to encrypted/password protected archives is not currently supported.

The 7-Zip format uses solid compression by default. Appending files to a solid archive requires that the entire archive will need to be decompressed and re-created, which could result in a significant performance penalty with large files or archives.

Compression is performed using [7-Zip](https://www.7-Zip.org).

## Related

[Decompress](./Decompress.md)

## Examples

Basic Compression

[Main]
Title=Compress Example 1
Author=Homes32
Description=Demonstrate usage of the Compress command.
Version=1
Level=5

[Interface]

[variables]

[process]
```pebakery
// PEBakery.ini will be compressed into Setting.zip.
Compress,Zip,%BaseDir%\PEBakery.ini,%BaseDir%\Setting.zip

// PEBakery.ini will be stored into Setting.7z.
Compress,7z,%BaseDir%\PEBakery.ini,%BaseDir%\Setting.7z,Store
```

This example saves the build log, then compresses the log and several ancillary log files into an archive that can be easily transported for debugging.

```
[Main]
Title=Compress Example 2
Author=Homes32
Description=Demonstrate usage of the Compress command.
Version=1
Level=5

[Interface]

[variables]

[process]
Echo,"Archiving Support Log...."
FileCreateBlank,%BaseDir%\Temp\myLog.log
FileCreateBlank,%BaseDir%\Temp\anotherLog.log
// Get a timestamp for our archive file name to avoid overwrites
StrFormat,DATE,%Timestamp%,"yyyy-mmm-dd-hhnn"
Echo,"Exporting Log as [HTML]..."
System,SaveLog,%BaseDir%\Temp\BuildLog.html
// Compress our build log and our other logs into a zip archive
Compress,Zip,%BaseDir%\Temp\*.log,%BaseDir%\%Timestamp%-%ProjectTitle%-Logs.zip
Compress,Zip,%BaseDir%\Temp\BuildLog.html,%BaseDir%\%Timestamp%-%ProjectTitle%-Logs.zip

Echo,"Done."
```