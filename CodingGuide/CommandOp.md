# Command Optimization

If enabled via **PEBakery >Settings > General > Optimize Code**, PEBakery will automatically optimize various commands related to file manipulation, however the optimization occurs only if the **same commands** that manipulate the **same file** are **placed in a row**.

When commands are optimized, multiple file read/write operations are compacted into single read/write operation, dramatically improving performance. In order to take advantage of this performance boost, make sure to place these commands together in your script.

## The following commands may be optimized

- TXTAddLine
- TXTReplace
- TXTDelLine
- INIRead
- INIWrite
- INIDelete
- INIReadSection
- INIAddSection
- INIDeleteSection
- INIWriteTextLine
- Visible
- ReadInterface
- WriteInterface
- WimExtract
- WimPathAdd
- WimPathDelete
- WimPathRename

## Error Handling for Optimized Commands

When optimization is turned off, all commands are processed independently. Even if one command fails it does not effect other commands. However, if commands are optimized, they affect all other commands in the same routine.

Let us assume a wim file `LZX.wim` contains these files:

```pebakery
LZX.wim
|--- AZ.txt
|--- B.txt
|--- Z.txt
```

In the code below, the second `WimExtract` statement tries to extract a non-existent file and will throw an error. Because these commands are internally executed as one `WimExtract` command, when an error thrown by the second file, it will cause the entire operation (all 3 WimExtract commands) to fail. It is the script author's responsibility to remain aware of how their commands will process and make sure the proper guards and error handling routines are in place for commands that will be optimized. In this example, using the `NOERR` flag on the WimExtract commands would prevent this situation, so long as it was acceptable to the author that a file wasn't extracted.

```pebakery
WimExtract,%WimDir%\LZX.wim,1,Z.txt,%DestDir%,CHECK
WimExtract,%WimDir%\LZX.wim,1,A.txt,%DestDir%,CHECK
WimExtract,%WimDir%\LZX.wim,1,B.txt,%DestDir%,CHECK
```

## Examples

### Example 1

TXTAddLine writes multiple lines into same file `%ProjectTemp%\Korean_IME_Reference.txt`. They are optimized to single internal command `TXTAddLineOp`, which writes all text in one operation.

```pebakery
Set,%w%,%ProjectTemp%\Korean_IME_Reference.txt
FileCreateBlank,%w%
TXTAddLine,%w%,"<Korean IME Script - Reference>",Append
TXTAddLine,%w%,,Append
TXTAddLine,%w%," [TechNet] Add Input Method Editor (IME) to Windows PE 3.0",Append
TXTAddLine,%w%,"  - https://technet.microsoft.com/en-us/library/dd744589%28v=ws.10%29.aspx",Append
TXTAddLine,%w%,,Append
TXTAddLine,%w%," [Blog] Add Hangul IME support on Windows PE 4.0",Append
TXTAddLine,%w%,"  - http://cappleblog.co.kr/549",Append
```

### Example 2

The Legacy `Visible` command will write all interface values to the script in a single write operation.

```pebakery
Visible,%pBevel3%,True,PERMANENT
Visible,%pCheckBox4%,True,PERMANENT
Visible,%pCheckBox5%,True,PERMANENT
Visible,%pCheckBox6%,True,PERMANENT
Visible,%pCheckBox7%,True,PERMANENT
```

### Example 3

TXTDelLine and TXTAddLine are different commands. No optimization will be performed.

```pebakery
TXTDelLine,%target_sys%\autorun.cmd,exit
TXTAddLine,%target_sys%\autorun.cmd,"hiderun.exe IMEReg.cmd",Append
```

Multiple TXTAddLine are writing to same file, however they are not placed in a row therefore no optimization will be performed.

```pebakery
TXTAddLine,%DestDir%\hello.txt,"Hello World!",Append
Echo,"Hello World!"
TXTAddLine,%DestDir%\hello.txt,"Have a nice day.",Append
```

These WimExtract handle same file, however they have different flags therefore no optimization will be performed.

``` pebakery
WimExtract,%WimDir%\LZX.wim,1,Z.txt,%DestDir%,CHECK
WimExtract,%WimDir%\LZX.wim,1,A?.txt,%DestDir%,NOACL
```
