# WriteInterface

Changes the properties of an interface control.

## Syntax

```pebakery
WriteInterface,<Property>,<ScriptFile>,<Interface>,<ControlName>,<Value>[,Delim=]
```

### Arguments

| Argument | Description |
| --- | --- |
| Property | The Property value to edit. Not all properties are applicable to all controls. See Control Specific Properties for details.
|| Text - Text value of the control. |
|| Visible - `True`/`False` - Show or Hide the control. |
|| PosX - Horizontal Position measured from the control's top left corner. |
|| PosY - Vertical Position measured from the control's top left corner. |
|| Width - Width of the control. |
|| Height - Height of the control. |
|| Value - Value of the control. |
|| Items - List of the items the control contains. |
|| Resource - The encoded file/picture assigned to the control. |
|| URL - Url assigned to the control. |
|| SectionName - Name of the section to run when a button is pushed or a value is changed. |
|| HideProgress - If `True` hide the run progress screen. If `False` show the run progress. |
|| ToolTip - Text that will be displayed when the user hovers over the control. Tooltips my be removed by specifying an empty string `""` or `NIL` as the tooltip value. |
| ScriptFile | The full path to the script. **Hint:** Use `%ScriptFile%` to reference the current script. |
| Interface | The name of the section containing the interface control you wish to modify. |
| ControlName | The name of the control to modify. |
| Value | The new value to write. |
| Delim= | **(Optional)** Delimiter used to separate the list of `Items` that will be written to a ComboBox or RadioGroup control. Case Insensitive. **Default:** `\|` |

### Control Specific Properties

#### Items Property

The `Items` Property is only supported in these controls:

| Control | Value |
| --- | --- |
| ComboBox     | (Delimited String) List of items to be assigned to the control. |
| RadioGroup   | (Delimited String) List of options to be assigned to the control. |

PEBakery assumes the `Items` list passed to the `WriteInterface` command is pipe `|` delimited unless otherwise specified by the `Delim=` argument.

Attempting to read `Items` from an unsupported control will result in an error.

#### Resource Property

The `Resource` Property is only supported in these controls:

| Control | Value |
| --- | --- |
| Button    | (String) The name of the embedded picture assigned to the control. |
| Image     | (String) The name of the embedded picture assigned to the control. |
| TextFile  | (String) The name of the embedded .txt/.rtf file assigned to the control. |

Resources must be embedded in the `InterfaceEncoded` section of the script where the Interface resides.

To clear the resource set the value to `Nil` or empty string `""`.

Attempting to read `Resource` from an unsupported control will result in an error.

#### Value Property

The `Value` Property is only supported in these controls:

| Control | Read Value |
| --- | --- |
| TextBox     | (String) Content of the control. |
| NumberBox   | (String) Content of the control. |
| CheckBox    | (Boolean) True/False, True if checked. |
| ComboBox    | (String) Selected item. |
| RadioButton | (Boolean) True/False, True if checked. |
| FileBox     | (String) Content of the control. |
| RadioGroup  | (Integer) Zero-Based Index of selected item. |

Attempting to write a `Value` to unsupported control will result an error.

#### URL Property

The `Url` Property is only supported in these controls:

| Control | Read Value |
| --- | --- |
| Image       | (String) URL. |
| WebLabel    | (String) URL. |

Attempting to write a `Url` to unsupported control will result an error.

#### SectionName Property

The `SectionName` property used for the Optional Engine Run is only supported in these controls:

| Control | Value |
| --- | --- |
| Button        | (String) Name of the script section to execute. |
| CheckBox      | (String) Name of the script section to execute. |
| ComboBox      | (String) Name of the script section to execute. |
| RadioButton   | (String) Name of the script section to execute. |
| RadioGroup    | (String) Name of the script section to execute. |

Attempting to read the `SectionName` property from an unsupported control will result in an error.

#### HideProgress Property

The `HideProgress` property used for the Optional Engine Run is only supported in these controls:

| Control | Value |
| --- | --- |
| Button        | (Boolean) If `True` hide the run progress screen. If `False` show the run progress. |
| CheckBox      | (Boolean) If `True` hide the run progress screen. If `False` show the run progress. |
| ComboBox      | (Boolean) If `True` hide the run progress screen. If `False` show the run progress. |
| RadioButton   | (Boolean) If `True` hide the run progress screen. If `False` show the run progress. |
| RadioGroup    | (Boolean) If `True` hide the run progress screen. If `False` show the run progress. |

Attempting to read the `HideProgress` property from an unsupported control will result in an error.

## Remarks

**Note:** It is not necessary to call `System,REFRESHINTERFACE` after a `WriteInterface` command.

## Related

[ReadInterface](./ReadInterface.md), [Script Interface Controls](../../GUIControls/README.md), [Set](../Control/Set.md), [Visible](./Visible.md)

## Examples

### Example 1

An interactive script demonstrating various usage.

```pebakery
[main]
Title=WriteInterface Example
Description=Show usage of WriteInterface
Level=5
Version=1
Author=Homes32

[variables]

[Process]

[Toggle_Advanced_Options]
System,CURSOR,WAIT
If,%SB_CfgProfile%,Equal,"Advanced",Begin
  WriteInterface,Visible,%ScriptFile%,Interface,BVL_AdvOptions,True
  WriteInterface,Visible,%ScriptFile%,Interface,LBL_AdvOptions,True
  WriteInterface,Visible,%ScriptFile%,Interface,CB_Adv1,True
  WriteInterface,Visible,%ScriptFile%,Interface,CB_Adv2,True
  WriteInterface,Visible,%ScriptFile%,Interface,BTN_SelectAll,True
  WriteInterface,Visible,%ScriptFile%,Interface,BTN_SelectNone,True
  WriteInterface,Visible,%ScriptFile%,Interface,LBL_Info,True
End
Else,Begin
  WriteInterface,Visible,%ScriptFile%,Interface,BVL_AdvOptions,False
  WriteInterface,Visible,%ScriptFile%,Interface,LBL_AdvOptions,False
  WriteInterface,Visible,%ScriptFile%,Interface,CB_Adv1,False
  WriteInterface,Visible,%ScriptFile%,Interface,CB_Adv2,False
  WriteInterface,Visible,%ScriptFile%,Interface,BTN_SelectAll,False
  WriteInterface,Visible,%ScriptFile%,Interface,BTN_SelectNone,False
  WriteInterface,Visible,%ScriptFile%,Interface,LBL_Info,False
End
System,CURSOR,NORMAL

[SelectAll]
WriteInterface,Value,%ScriptFile%,Interface,CB_Adv1,True
WriteInterface,Value,%ScriptFile%,Interface,CB_Adv2,True
WriteInterface,Text,%ScriptFile%,Interface,LBL_Info,"All Options Selected!"

[SelectNone]
WriteInterface,Value,%ScriptFile%,Interface,CB_Adv1,False
WriteInterface,Value,%ScriptFile%,Interface,CB_Adv2,False
WriteInterface,Text,%ScriptFile%,Interface,LBL_Info,"All Options Disabled!"

[ReadValues]
// Read Visibility
ReadInterface,Visible,%ScriptFile%,Interface,CB_Adv1,%value%
Message,"The Option 1 check box is Visible: %value%"

// Read value
ReadInterface,Value,%ScriptFile%,Interface,CB_Adv1,%value%
Message,"The Option 1 check box is Checked: %value%"

// Read Text
ReadInterface,Text,%ScriptFile%,Interface,CB_Adv1,%value%
Message,"The Option 1 check box caption is: %value%"

// Read Dimensions
ReadInterface,Height,%ScriptFile%,Interface,CB_Adv1,%height%
ReadInterface,Width,%ScriptFile%,Interface,CB_Adv1,%width%
Message,"The Option 1 check box dimensions are : %width%x%height%"

// Read Position
ReadInterface,PosX,%ScriptFile%,Interface,CB_Adv1,%x%
ReadInterface,PosY,%ScriptFile%,Interface,CB_Adv1,%y%
Message,"The Option 1 check box is located at : %x%#$c%y%"

// Text box
ReadInterface,Text,%ScriptFile%,Interface,TXT_FilePath,%text%
ReadInterface,Value,%ScriptFile%,Interface,TXT_FilePath,%value%
Message,"Text box name: %text% #$x Text box value: %value%"

[BumpLeft]
// Move the textbox to the left
ReadInterface,PosX,%ScriptFile%,Interface,TXT_MoveMe,%x%
ReadInterface,PosY,%ScriptFile%,Interface,TXT_MoveMe,%y%
StrFormat,DEC,%x%,1
WriteInterface,PosX,%ScriptFile%,Interface,TXT_MoveMe,%x%
WriteInterface,Text,%ScriptFile%,Interface,LBL_X,%x%
WriteInterface,Text,%ScriptFile%,Interface,LBL_Y,%y%

[BumpRight]
// Move the textbox to the right
ReadInterface,PosX,%ScriptFile%,Interface,TXT_MoveMe,%x%
ReadInterface,PosY,%ScriptFile%,Interface,TXT_MoveMe,%y%
StrFormat,INC,%x%,1
WriteInterface,PosX,%ScriptFile%,Interface,TXT_MoveMe,%x%
WriteInterface,Text,%ScriptFile%,Interface,LBL_X,%x%
WriteInterface,Text,%ScriptFile%,Interface,LBL_Y,%y%

[Shrink]
// Make the textbox smaller
ReadInterface,Width,%ScriptFile%,Interface,TXT_MoveMe,%width%
ReadInterface,Height,%ScriptFile%,Interface,TXT_MoveMe,%height%
StrFormat,DEC,%width%,1
StrFormat,DEC,%height%,1
WriteInterface,Width,%ScriptFile%,Interface,TXT_MoveMe,%width%
WriteInterface,Height,%ScriptFile%,Interface,TXT_MoveMe,%height%
WriteInterface,Text,%ScriptFile%,Interface,LBL_WidthValue,%width%
WriteInterface,Text,%ScriptFile%,Interface,LBL_HeightValue,%height%

[Grow]
// Make the textbox larger
ReadInterface,Width,%ScriptFile%,Interface,TXT_MoveMe,%width%
ReadInterface,Height,%ScriptFile%,Interface,TXT_MoveMe,%height%
StrFormat,INC,%width%,1
StrFormat,INC,%height%,1
WriteInterface,Width,%ScriptFile%,Interface,TXT_MoveMe,%width%
WriteInterface,Height,%ScriptFile%,Interface,TXT_MoveMe,%height%
WriteInterface,Text,%ScriptFile%,Interface,LBL_WidthValue,%width%
WriteInterface,Text,%ScriptFile%,Interface,LBL_HeightValue,%height%

[Interface]
LBL_CfgProfile="Configuration Profile:",1,1,12,16,120,20,8,Bold
SB_CfgProfile=Advanced,1,4,135,10,150,21,Simple,Advanced,_Toggle_Advanced_Options_,True
TXT_FilePath="File Path",1,0,16,78,200,21,C:\Temp
BVL_AdvOptions=pBevel1,1,12,9,114,170,88,
LBL_AdvOptions="Advanced Options:",1,1,23,120,147,18,8,Bold
CB_Adv1="Option 1",1,3,20,150,145,20,True
CB_ADV2="Option 2",1,3,20,170,135,20,True
BTN_SelectAll="Select All",1,8,94,146,80,25,SelectAll,0,True
BTN_SelectNone="Select None",1,8,94,170,80,25,SelectNone,0,True
LBL_Info="All Options Selected!",1,1,10,206,170,18,8,Bold
BTN_ReadValues="Read Values",1,8,200,135,147,48,ReadValues,0,True
BTN_BumpLeft=<<,1,8,170,276,80,25,BumpLeft,0,True
BTN_BumpRight=>>,1,8,261,276,80,25,BumpRight,0,True
TXT_MoveMe="Use buttons to change me!",1,0,154,247,200,21,abc..
BTN_Shrink=Shrink,1,8,170,303,80,25,Shrink,0,True
BTN_Grow=Grow,1,8,261,303,80,25,Grow,0,True
pBevel1=pBevel1,1,12,146,334,211,40
LBL_PosX="PosX: ",1,1,152,339,32,18,8,Normal
LBL_PosY=PosY:,1,1,151,360,33,18,8,Normal
LBL_X=154,1,1,186,339,58,18,8,Normal
LBL_Y=247,1,1,186,360,58,18,8,Normal
LBL_Width=Width:,1,1,259,339,39,18,8,Normal
LBL_Height=Height:,1,1,258,360,40,18,8,Normal
LBL_WidthValue=200,1,1,301,340,50,18,8,Normal
LBL_HeightValue=21,1,1,301,360,50,18,8,Normal
```

### Example 2

Let us assume a file %ScriptFile% consists of these sections:

```pebakery
[Main]
Title=WriteInterface
Author=ied206
Description=UnitTest
Version=001
Level=5

[Interface]
pTextBox1=Display,1,0,20,20,200,21,StringValue
pTextLabel1=Display,1,1,20,50,230,18,8,Normal
pNumberBox1=pNumberBox1,1,2,20,70,40,22,3,0,100,1
pCheckBox1=pCheckBox1,1,3,20,100,200,18,True
pComboBox1=A,1,4,20,130,150,21,A,B,C,D
pRadioGroup1=pRadioGroup1,1,14,20,160,150,60,Option1,Option2,Option3,0
pImage1=Logo.jpg,1,5,20,230,40,40,
pTextFile1=HelpMsg.txt,1,6,240,20,200,86
pButton1=ShowProgress,1,8,240,115,80,25,Hello,0,False,False,_Hello_,False
pButton2=HideProgress,1,8,330,115,80,25,Hello,0,True,_Hello_,True
pWebLabel1=GitHub,1,10,250,160,32,18,https://github.com/ied206/PEBakery
pRadioButton1=pRadioButton1,1,11,250,180,100,20,False
pBevel1=pBevel1,1,12,240,150,235,60
pFileBox1=C:\Windows\notepad.exe,1,13,240,230,200,20,file
pFileBox2=E:\WinPE\,1,13,240,260,200,20,dir
pTextLabel2=Hidden,0,1,20,50,280,18,8,Normal
```

#### Write Text

```pebakery
// Source : pTextBox1=Display,1,0,20,20,200,21,StringValue
// Result : pTextBox1=PEBakery,1,0,20,20,200,21,StringValue
WriteInterface,Text,%ScriptFile%,Interface,pTextBox1,PEBakery
```

#### Write Items

Replace `A,B,C,D` items with `D,C,B,A`

```pebakery
// Source : pComboBox1=A,1,4,20,130,150,21,A,B,C,D
// Result : pComboBox1=B,1,4,20,130,150,21,D,C,B,A
WriteInterface,Items,%ScriptFile%,Interface,pComboBox1,D|C|B|A
```

Append  `D,C,B,A` to the existing list of items

```pebakery
// Source : pComboBox1=A,1,4,20,130,150,21,A,B,C,D
// Result : pComboBox1=B,1,4,20,130,150,21,A,B,C,D,D,C,B,A

// Get the current items in pComboBox1
ReadInterface,Items,%ScriptFile%,Interface,pComboBox1,%ExistingItems%
// Append to our new list and write
WriteInterface,Items,%ScriptFile%,Interface,pComboBox1,%ExistingItems%|D|C|B|A
```

#### Write Visibility

```pebakery
// Source : pTextLabel1=Display,1,1,20,50,230,18,8,Normal
// Result : pTextLabel1=Display,0,1,20,50,230,18,8,Normal
WriteInterface,Visible,%ScriptFile%,Interface,pTextLabel1,False
```

#### Write Value

```pebakery
// Source : pTextBox1=Display,1,0,20,20,200,21,StringValue
// Result : pTextBox1=Display,1,0,20,20,200,21,PEBakery
WriteInterface,Value,%ScriptFile%,Interface,pTextBox1,PEBakery

// Source : pNumberBox1=pNumberBox1,1,2,20,70,40,22,3,0,100,1
// Result : pNumberBox1=pNumberBox1,1,2,20,70,40,22,2,0,100,1
WriteInterface,Value,%ScriptFile%,Interface,pNumberBox1,2

// Source : pNumberBox1=pNumberBox1,1,2,20,70,40,22,3,0,100,1
// Result : pNumberBox1=pNumberBox1,1,2,20,70,40,22,2,0,100,1
WriteInterface,Value,%ScriptFile%,Interface,pCheckBox1,%Dest%

// Source : pComboBox1=A,1,4,20,130,150,21,A,B,C,D
// Result : pComboBox1=B,1,4,20,130,150,21,A,B,C,D
WriteInterface,Value,%ScriptFile%,Interface,pComboBox1,B

// Source : pRadioButton1=pRadioButton1,1,11,250,180,100,20,False
// Result : pRadioButton1=pRadioButton1,1,11,250,180,100,20,True
WriteInterface,Value,%ScriptFile%,Interface,pRadioButton1,True

// Source : pFileBox1=C:\Windows\notepad.exe,1,13,240,230,200,20,file
// Result : pFileBox1=D:\PEBakery\Launcher.exe,1,13,240,230,200,20,file
WriteInterface,Value,%ScriptFile%,Interface,pFileBox1,D:\PEBakery\Launcher.exe

// Source : pRadioGroup1=pRadioGroup1,1,14,20,160,150,60,Option1,Option2,Option3,2
// Result : pRadioGroup1=pRadioGroup1,1,14,20,160,150,60,Option1,Option2,Option3,0
WriteInterface,Value,%ScriptFile%,Interface,pRadioGroup1,0
```
