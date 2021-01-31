# ShellExecute

Runs an external program and waits for it to terminate before processing continues.

## Syntax

```pebakery
ShellExecute,<Action>,<FilePath>[,Params][,WorkDir][,%ExitOutVar%]
```

### Arguments

| Argument | Description |
| --- | --- |
| Action | The method used to start the external file. Can be one of the following: |
|| Open - If the file is an executable it will be launched. If the file is not an executable it will be opened using the default application associated with that file type.  |
|| Hide - The file will be launched in hidden mode. Console programs writing to the StdOut and StdErr streams will have their output redirected to PEBakerys build window and written to the log. |
|| Print - Print the contents of the file using the systems default printer. |
|| Explore - Open an explorer window. (Can be used to display the contents of the local file system.) |
|| Min - Same as Open, but starts the program minimized to the taskbar. |
| FilePath | The file to execute. If a full path is not specified PEBakery will attempt to locate it using the operating system's %PATH% variable. |
| Params | **(Optional)** Any arguments you wish to pass to the program. Use ("") for none. |
| WorkDir | **(Optional)** The working directory for the program. Use ("") to specify the current working directory. |
| %ExitOutVar% | **(Optional)** Variable that will be updated with the *Exit Code* returned by the application. This can be used to validated a successful execution or return a value to the script for further processing. If you do not specify this argument you can still read the *Exit Code* from the fixed `%ExitCode%` variable. |

### Return Codes

| Variable | Description |
| --- | --- |
| %ExitCode% | (Legacy) Contains the *Exit Code* returned by the most recent `ShellExecute` command. |
| #r | Contains the *Exit Code* returned by the most recent `ShellExecute` command. |

`%ExitCode%` is included for compatibility with Winbuilder 082.

## Remarks

**Warning:** Using the `Hide` action with an application that does not exit automatically when finished will cause the script to hang until you manually end the process.

## Related

[ShellExecuteDelete](./ShellExecuteDelete.md), [ShellExecuteEx](./ShellExecuteEx.md), [Variables](../../LangRef/Variables.md)

## Examples

### Example 1

```pebakery
[Main]
Title=ShellExecute Example
Author=Homes32
Description=Demonstrate usage of the ShellExecute command.
Version=1
Level=5

[Interface]

[variables]

[process]

// "Open" a program that stays open until closed.
Echo,"Running notepad.exe...#$xYou must close the notepad application in order to continue processing."
ShellExecute,open,notepad.exe

// "Open" a program that will exit when it is finished.
Echo,"Running a console application with the OPEN action is annoying!#$xPlease use the HIDE action unless your application require user input!"
ShellExecute,open,cmd.exe,"/C PING 127.0.0.1 -n 10","",%return%
Message,"ShellExecute returned: %return%"

// Run a program "Hidden" that will exit when it is finished.
Echo,"Running a console application requiring no user input with the HIDE action to prevent annoying pop-up boxes and keep the user from accidentally closing the program before it is finished.#$xIt also allows us to see the result of the program in the log."
ShellExecute,hide,cmd.exe,"/C PING 127.0.0.1 -n 10","",%return%
Message,"ShellExecute returned: %return%"

// "Open" a program "Minimized".
Echo,"Running a console application minimized..."
ShellExecute,min,cmd.exe,"/C PING 127.0.0.1 -n 10","",%return%
Message,"ShellExecute returned: %return%"
```