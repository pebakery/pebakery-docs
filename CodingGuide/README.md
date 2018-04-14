# Coding Guide

## Syntax Checking

PEBakery supports syntax checking.

### Checking Statements or Section

Copy codes into `Syntax Checker` provided in `Utility`.

### Checking Plugin

Make sure your plugin is visible in project tree. Open plugin's interface, and click the question button near script title.

If `Auto Syntax Check Error` setting is enabled, the button's icon and color reports if error exists.

## Optimization

PEBakery automatically optimizes some commands related to text manipulation.

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
- WimExtract
- WimPathAdd, WimPathDelete, WimPathRename

When commands are optimized, multiple file read/write is compacted into single read/write, improving performance.

The optimization occurs only if **same commands** manipulates **same file** are **placed in a row**.

Make sure your code can be optimized for performance.

### Example of Optimized Commands

TXTAddLine writes multiple lines into same file `%ProjectTemp%\Korean_IME_Reference.txt`. They are optimized to single command TXTAddLineOp, writing full text at once.

```pebakery
Set,%w%,%ProjectTemp%\Korean_IME_Reference.txt
FileCreateBlank,%w%
TXTAddLine,%w%,"<Korean IME Plugin - Reference>",Append
TXTAddLine,%w%,,Append
TXTAddLine,%w%," [TechNet] Add Input Method Editor (IME) to Windows PE 3.0",Append
TXTAddLine,%w%,"  - https://technet.microsoft.com/en-us/library/dd744589%28v=ws.10%29.aspx",Append
TXTAddLine,%w%,,Append
TXTAddLine,%w%," [Blog] Add Hangul IME support on Windows PE 4.0",Append
TXTAddLine,%w%,"  - http://cappleblog.co.kr/549",Append
```

Visible command only affects plugin itself.

```pebakery
Visible,%pBevel3%,True,PERMANENT
Visible,%pCheckBox4%,True,PERMANENT
Visible,%pCheckBox5%,True,PERMANENT
Visible,%pCheckBox6%,True,PERMANENT
Visible,%pCheckBox7%,True,PERMANENT
```

### Example of Non-Optimized Commands

TXTDelLine and TXTAddLine are different command.

```pebakery
TXTDelLine,%target_sys%\autorun.cmd,exit
TXTAddLine,%target_sys%\autorun.cmd,"hiderun.exe IMEReg.cmd",Append
```

Multiple TXTAddLine are writing to same file, but they are not placed in a row.

```pebakery
TXTAddLine,%DestDir%\hello.txt,"Hello World!",Append
Echo,"Hello World!"
TXTAddLine,%DestDir%\hello.txt,"Have a nice day.",Append
```

These WimExtract handle same file, but they have different flags.

``` pebakery
WimExtract,%WimDir%\LZX.wim,1,Z.txt,%DestDir%,CHECK
WimExtract,%WimDir%\LZX.wim,1,A?.txt,%DestDir%,NOACL
```

### Possible Problem with Optimization

When optimization is turned off, a command is independent from others. Which means even if one command failed, it does not effect other commands. But if commands are optimized, it do effect other commands.

Let us assume a wim file `LZX.wim` contains these files:

```pebakery
LZX.wim
|--- AZ.txt
|--- B.txt
|--- Z.txt
```

Second WimExtract tries to extract non-existent file, so it will throw an error. These commands are optimized to one command when executed, and error throwed by second WimExtract will cause all WimExtracts to fail.

```pebakery
WimExtract,%WimDir%\LZX.wim,1,Z.txt,%DestDir%,CHECK
WimExtract,%WimDir%\LZX.wim,1,B.txt,%DestDir%,CHECK
WimExtract,%WimDir%\LZX.wim,1,A.txt,%DestDir%,CHECK
```
