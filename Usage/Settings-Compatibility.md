# Compatibility Settings

## Asterisk Bug

| Setting | Description |
| --- | --- |
| Simulate WinBuilder's *.* bug in DirCopy | When using wildcards to copy subdirectories, files that exist at the same level are copied as well. |
| Simulate WinBuilder's *.* bug in folder.project | When using wildcards to find folder links, scripts in the root of the specified folder are ignored and only scripts in sub-folders are loaded. |

## Command

| Setting | Description |
| --- | --- |
| FileRename and DirMove work like PathMove | Allows `FileRename` and `DirMove` command to move files. |
| Allow letter in Loop | Allows the Loop command to increment alphabetically as well as numerically.|
| Enable depreciated legacy branch conditions | Allow legacy conditions such as `NOTEXISTFILE`, `NOTEXISTDIR`, etc. (Replaced by `If,Not,ExistFile`)|
| Allow variables in RegWrite's `<HKey>`, `<ValueType>` argument | Allows variables to be used as arguments in RegWrite. |
| Allow Set to modify interface controls | Allows the `Set` command to write values to interface controls. (eg. Textlabel value). (Replaced by `WriteInterface,Value...`) |
| Enable legacy interface commands (eg. Visible) | Enable legacy commands such as `Visible`. (Replaced by `WriteInterface,Visible...`)|
| Enable legacy section parameter commands e.g. GetParam, PackParam) | Allows you to use the depreciated `GetParam` and `PackParam` commands. |

## Script Interface

| Setting | Description |
| --- | --- |
| Ignore width of WebLabel | WinBuilder ignores the specified width of WebLabel controls and sizes them to fit the text. Use this option to replicate this behavior. |

## Variable

| Setting | Description |
| --- | --- |
| Overridable fixed variables | Allow constant/fixed variables to be overwritten. |
| Enable environment variables | Enable a limited set of pre-define environment variables. |
| Disable extended section parameters (g.g. #a, #r) | Disables the `#a` and `#r` tokens. This may be desirable if you use statements such as `TxtAddline,%w%,"#RequireAdmin",Append` where PEBakery can mistake `#R`  for the `#r` token.   |