# Operators

PEBakery supports the following comparison and logical operators.

## Comparison Operators

These operators are used in conjunction with the `If` command to compare values. If the test returns true, then a Command is executed.

| Operator | Description |
| --- | --- |
| Equal<br/>== | Tests if two values are equal. e.g. `If,%var%,==,5,<Command>` (true if %Var% equals 5). Case insensitive when used with strings. |
| EqualX | Tests if two strings are equal. Case sensitive. The left and right values are converted to strings if they are not strings already. This operator should only be used if string comparisons need to be case sensitive. |
| != | Tests if two values are not equal. Case insensitive when used with strings. To do a case sensitive not equal comparison use `If,Not,%var1%,EqualX,%var2%,<Command>` |
| Smaller<br/>< | Tests if the first value is less than the second. |
| SmallerEqual<br/><= | Tests if the first value is less than or equal to the second. |
| Bigger<br/>> | Tests if the first value is greater than the second. |
| BiggerEqual<br/>>= | Tests if the first value is greater than or equal to the second. |

## Conditional Tests

These tests are used in conjunction with the `If` command to determine if a file, directory, script section, registry value, macro, variable, or network connection does or does not exist. If the test returns true, then a Command is executed. Based on the specific test selected, one or more additional arguments may be needed.

| Test | Description |
| --- | --- |
| ExistFile | Checks to see if a file exists. |
| ExistDir | Checks to see if a directory exists. |
| ExistSection | Checks to see if a [Section] exists within a file. |
| ExistRegSubKey<br/>ExistRegSection | Checks to see if a key exists within a registry hive. `ExistRegSection` is supported for backwards compatibility with Winbuilder scripts, however newer scripts should use the more accurately named `ExistRegSubKey` command instead. |
| ExistRegValue<br/>ExistRegKey | Checks to see if a value exists within a registry hive. `ExistRegKey` is supported for backwards compatibility with Winbuilder scripts, however newer scripts should use the more accurately named `ExistRegValue` command instead. |
| ExistRegMulti | Checks for the existence of a substring in a multiple string value. |
| ExistVar | Checks to see if a variable is defined. |
| ExistMacro | Checks to see if a macro is defined. |
| Online | Checks to see if the computer has an active network connection. |
| Ping | Checks to see if a remote host can be reached by sending an ICMP echo-request to a specified host. Returns true if a valid ICMP echo-response is received. *Note: The presence and configuration of proxies, network address translation (NAT) equipment, or firewalls can prevent Ping from succeeding.* |
| WimExistIndex | Checks to see if the specified Index exists within a WIM file. Split WIMs (.swm) are supported. |
| WimExistFile | Checks to see if a file exists within a WIM file. Split WIMs (.swm) are supported. |
| WimExistDir | Checks to see if a directory exists within a WIM file. Split WIMs (.swm) are supported. |

## Logic Operators

| Operator | Description |
| --- | --- |
| Not | Logical Not operation. |

## Remarks

**All tests can be negatived by prefixing the logical `Not` operator to the conditional test.**

## Related

[If](./If.md), [If-Else](./If-Else.md), [If,Question](./If-Question.md)

## Examples

### Example 1

```pebakery
[Main]
Title=Operators
Description=Show the operators PEBakery supports.
Level=5
Version=1
Author=Homes32

[Variables]
%Value1%=1
%Value2%=2
%Value3%="Hello World!"
%Value4%="HeLlO wOrLd!"
myMacro=Message,"I'm A Macro!"

[process]
// Change the values of the variables above to see different results with the following commands.

// Syntax: If,<Value1>,Bigger,<Value2>,<Command>
If,%Value1%,Bigger,%Value2%,Message,"%Value1% is bigger then %Value2%"

// Syntax: If,<Value1>,BiggerEqual,<Value2>,<Command>
If,%Value1%,BiggerEqual,%Value2%,Message,"%Value1% is equal to or bigger then %Value2%"

// Syntax: If,<Value1>,Equal,<Value2>,<Command>
If,%Value1%,Equal,%Value2%,Message,"%Value1% is equal to %Value2%"

// Syntax: If,<Value1>,EqualX,<Value2>,<Command>
If,Not,%Value3%,EqualX,%Value4,Message,"%Value3%#$xis not equal to#$x%Value4%"

// For Not-Equal tests we can use either the != operator or negate the Equal command.
// Syntax: If,<Value1>,!=,<Value2>,<Command>
If,%Value1%,!=,%Value2%,Message,"%Value1% is != to %Value2%"
// Syntax: If,Not,<Value1>Equal,<Value2>,<Command>
If,Not,%Value1%,Equal,%Value2%,Message,"%Value1% is not equal to %Value2%"

// Syntax: If,<Value1>,Smaller,<Value2>,<Command>
If,%Value2%,Smaller,%Value1%,Message,"%Value2% is smaller then %Value1%"

// Syntax: If,<Value1>,SmallerEqual,<Value2>,<Command>
If,%Value2%,SmallerEqual,%Value1%,Message,"%Value2% is equal to or smaller then %Value1%"

// Syntax: If,ExistDir,<DirPath>,<Command>
If,ExistDir,C:\Temp,Message,"C:\Temp Exists"

// Syntax: If,ExistFile,<FilePath>,<Command>
If,ExistFile,C:\Temp\myFile.txt,Message,"C:\Temp\myFile.txt Exists"

// Syntax: If,ExistMacro,<Macro>,<Command>
If,ExistMacro,myMacro,Message,"myMacro Exists!"

// Syntax: If,ExistRegValue,<HKey>,<KeyPath>,<ValueName>
If,ExistRegValue,HKLM,SOFTWARE\Microsoft\Windows NT\CurrentVersion,ProductName,Message,"Registry value exists"

// Syntax: If,ExistRegMulti,<HKey>,<KeyPath>,<ValueName>,<SubValue>,<Command>
If,ExistRegMulti,HKLM,System\ControlSet001\Control\Class\{71A27CDD-812A-11D0-BEC7-08002BE2092F},UpperFilters,volsnap,Message,"volsnap exists in RegMulti UpperFilters"

// Syntax: If,ExistRegSubKey,<HKey>,<KeyPath>,<Command>
If,ExistRegSubKey,HKLM,SOFTWARE\Microsoft\Windows NT\CurrentVersion,Message,"Registry key exists"

// Syntax: If,ExistSection,<FileName>,<Section>,<Command>
If,ExistSection,%ScriptFile%,Process,Message,"Process section exists in %ScriptFile%"

// Syntax: If,ExistVar,<Variable>,<Command>
If,ExistVar,%Value1%,Message,"Variable: #$pValue1#$p exists"

// Syntax: If,Online,<Command>
If,Online,Message,"Network Connection Found"

// Ping can use either IP or DNS name.
// Syntax: If,Ping,<Dest>,<Command>
If,Ping,127.0.0.1,Message,"I can ping 127.0.0.1"
If,Ping,google.com,Message,"I can ping google.com"

// Syntax: If,WimExistIndex,<SrcWim>,<ImageIndex>
If,WimExistIndex,C:\Temp\boot.wim,1,Message,"The Index exists"

// Syntax: If,WimExistDir,<SrcWim>,<ImageIndex>,<DirPath>
If,WimExistDir,C:\Temp\boot.wim,1,Windows\System32,Message,"The Directory exists within the WIM image."

// Syntax: If,WimExistFile,<SrcWim>,<ImageIndex>,<FilePath>
If,WimExistFile,C:\Temp\boot.wim,1,Windows\regedit.exe,Message,"The File exists within the WIM image."

```