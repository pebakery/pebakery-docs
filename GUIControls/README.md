# Script Interface Controls

Interface Controls allow you to dynamically interact with a script.

Controls must be placed in one or more dedicated interface `[Sections]` and cannot be mixed with other commands.

## Controls

The following control types are support by PEBakery.

Click on the control's name in the table below for details on each control.

| ID | Name | Description |
| :---: | --- | --- |
| 0 | [Text Box](./TextBox.md) | An input box that accepts a single line of text. |
| 1 | [Text Label](./TextLabel.md) | Displays a line of text. |
| 2 | [Number Box](./NumberBox.md) | An input box that accepts a number between a given minimum and maximum range. |
| 3 | [Check Box](./CheckBox.md) | A box that can be "checked" or "unchecked". |
| 4 | [Combo Box](./ComboBox.md) | A drop-down list allowing you to select a single value. |
| 5 | [Image](./Image.md) | Displays an image embedded within the script. |
| 6 | [Text File](./TextFile.md) | Displays a text file embedded within the script. |
| 7 | Text Edit | **Not Implemented** - Alternatives, such as launching the file with *notepad.exe* are more flexible. |
| 8 | [Button](./Button.md) | A simple button that can be used to run a section of code within the script. |
| 9 | Check List | **Not Implemented** - Not enough interest. Limited use cases. |
| 10 | [Web Label](./WebLabel.md) | A hyperlink that will open a webpage in the default browser. |
| 11 | [Radio Button](./RadioButton.md) | A circular button that can have only one radio button selected on the interface at a time. |
| 12 | [Bevel](./Bevel.md) | A rectangular frame used to organize controls. |
| 13 | [File Box](./FileBox.md) | An input box with a browse button that allows you to select a file or directory. |
| 14 | [Radio Group](./RadioGroup.md) | A group of radio buttons. Only one radio button per group may be selected at a time. |

## Remarks

Z-Index: PEBakery draws controls in the order they are defined in the interface section. Controls defined further down the section have a greater stack order and are always placed in front of controls with a lower stack order.

## Related

[AddInterface](/Commands/Interface/AddInterface), [RefreshInterface](/Commands/System/RefreshInterface), [ReadInterface](/Commands/Interface/ReadInterface.md), [WriteInterface](/Commands/Interface/WriteInterface.md)

## Examples

### Example 1

The following script shows examples of each control.

```pebakery
[main]
Title=Interface Controls
Description=Interface Controls Example
Author=Homes32
Level=5
Version=1

[variables]

[process]

[ShowSelectedControl]
System,Cursor,Wait
Run,%ScriptFile%,HideEverything
If,%RG_SelectControl%,Equal,0,WriteInterface,Visible,%ScriptFile%,Interface,TextBox1,True
If,%RG_SelectControl%,Equal,1,Begin
  WriteInterface,Visible,%ScriptFile%,Interface,TextLabel1,True
  WriteInterface,Visible,%ScriptFile%,Interface,TextLabel2,True
  WriteInterface,Visible,%ScriptFile%,Interface,TextLabel3,True
  WriteInterface,Visible,%ScriptFile%,Interface,TextLabel4,True
  WriteInterface,Visible,%ScriptFile%,Interface,TextLabel5,True
  WriteInterface,Visible,%ScriptFile%,Interface,TextLabel6,True
  WriteInterface,Visible,%ScriptFile%,Interface,TextLabel7,True
End
If,%RG_SelectControl%,Equal,2,Begin
  WriteInterface,Visible,%ScriptFile%,Interface,NumberBox1,True
  WriteInterface,Visible,%ScriptFile%,Interface,NumberBox2,True
End
If,%RG_SelectControl%,Equal,3,WriteInterface,Visible,%ScriptFile%,Interface,CheckBox1,True
If,%RG_SelectControl%,Equal,4,WriteInterface,Visible,%ScriptFile%,Interface,ComboBox1,True
If,%RG_SelectControl%,Equal,5,WriteInterface,Visible,%ScriptFile%,Interface,Image1,True
If,%RG_SelectControl%,Equal,6,WriteInterface,Visible,%ScriptFile%,Interface,TextFile1,True
If,%RG_SelectControl%,Equal,7,Begin
  WriteInterface,Visible,%ScriptFile%,Interface,Button1,True
  WriteInterface,Visible,%ScriptFile%,Interface,Button2,True
End
If,%RG_SelectControl%,Equal,8,WriteInterface,Visible,%ScriptFile%,Interface,WebLabel1,True
If,%RG_SelectControl%,Equal,9,Begin
  WriteInterface,Visible,%ScriptFile%,Interface,RadioButton1,True
  WriteInterface,Visible,%ScriptFile%,Interface,RadioButton2,True
  WriteInterface,Visible,%ScriptFile%,Interface,RadioButton3,True
End
If,%RG_SelectControl%,Equal,10,WriteInterface,Visible,%ScriptFile%,Interface,Bevel2,True
If,%RG_SelectControl%,Equal,11,Begin
  WriteInterface,Visible,%ScriptFile%,Interface,FileBox1,True
  WriteInterface,Visible,%ScriptFile%,Interface,FileBox2,True
  WriteInterface,Visible,%ScriptFile%,Interface,TextLabel6,True
  WriteInterface,Visible,%ScriptFile%,Interface,TextLabel7,True
End
If,%RG_SelectControl%,Equal,12,WriteInterface,Visible,%ScriptFile%,Interface,RadioGroup1,True
If,%RG_SelectControl%,Equal,13,Run,%ScriptFile%,ShowEverything
System,Cursor,Normal

[HideEverything]
WriteInterface,Visible,%ScriptFile%,Interface,TextBox1,False
WriteInterface,Visible,%ScriptFile%,Interface,TextLabel1,False
WriteInterface,Visible,%ScriptFile%,Interface,TextLabel2,False
WriteInterface,Visible,%ScriptFile%,Interface,TextLabel3,False
WriteInterface,Visible,%ScriptFile%,Interface,TextLabel4,False
WriteInterface,Visible,%ScriptFile%,Interface,TextLabel5,False
WriteInterface,Visible,%ScriptFile%,Interface,NumberBox1,False
WriteInterface,Visible,%ScriptFile%,Interface,NumberBox2,False
WriteInterface,Visible,%ScriptFile%,Interface,CheckBox1,False
WriteInterface,Visible,%ScriptFile%,Interface,ComboBox1,False
WriteInterface,Visible,%ScriptFile%,Interface,Image1,False
WriteInterface,Visible,%ScriptFile%,Interface,TextFile1,False
WriteInterface,Visible,%ScriptFile%,Interface,Button1,False
WriteInterface,Visible,%ScriptFile%,Interface,Button2,False
WriteInterface,Visible,%ScriptFile%,Interface,WebLabel1,False
WriteInterface,Visible,%ScriptFile%,Interface,RadioButton1,False
WriteInterface,Visible,%ScriptFile%,Interface,RadioButton2,False
WriteInterface,Visible,%ScriptFile%,Interface,RadioButton3,False
WriteInterface,Visible,%ScriptFile%,Interface,Bevel2,False
WriteInterface,Visible,%ScriptFile%,Interface,FileBox1,False
WriteInterface,Visible,%ScriptFile%,Interface,FileBox2,False
WriteInterface,Visible,%ScriptFile%,Interface,TextLabel6,False
WriteInterface,Visible,%ScriptFile%,Interface,TextLabel7,False
WriteInterface,Visible,%ScriptFile%,Interface,RadioGroup1,False

[ShowEverything]
WriteInterface,Visible,%ScriptFile%,Interface,TextBox1,True
WriteInterface,Visible,%ScriptFile%,Interface,TextLabel1,True
WriteInterface,Visible,%ScriptFile%,Interface,TextLabel2,True
WriteInterface,Visible,%ScriptFile%,Interface,TextLabel3,True
WriteInterface,Visible,%ScriptFile%,Interface,TextLabel4,True
WriteInterface,Visible,%ScriptFile%,Interface,TextLabel5,True
WriteInterface,Visible,%ScriptFile%,Interface,NumberBox1,True
WriteInterface,Visible,%ScriptFile%,Interface,NumberBox2,True
WriteInterface,Visible,%ScriptFile%,Interface,CheckBox1,True
WriteInterface,Visible,%ScriptFile%,Interface,ComboBox1,True
WriteInterface,Visible,%ScriptFile%,Interface,Image1,True
WriteInterface,Visible,%ScriptFile%,Interface,TextFile1,True
WriteInterface,Visible,%ScriptFile%,Interface,Button1,True
WriteInterface,Visible,%ScriptFile%,Interface,Button2,True
WriteInterface,Visible,%ScriptFile%,Interface,WebLabel1,True
WriteInterface,Visible,%ScriptFile%,Interface,RadioButton1,True
WriteInterface,Visible,%ScriptFile%,Interface,RadioButton2,True
WriteInterface,Visible,%ScriptFile%,Interface,RadioButton3,True
WriteInterface,Visible,%ScriptFile%,Interface,Bevel2,True
WriteInterface,Visible,%ScriptFile%,Interface,FileBox1,True
WriteInterface,Visible,%ScriptFile%,Interface,FileBox2,True
WriteInterface,Visible,%ScriptFile%,Interface,TextLabel6,True
WriteInterface,Visible,%ScriptFile%,Interface,TextLabel7,True
WriteInterface,Visible,%ScriptFile%,Interface,RadioGroup1,True

[Interface]
RG_SelectControl="Choose a Control",1,14,4,5,120,290,"Text Box","Text Label","Number Box","Check Box","Combo Box",Image,"Text File",Button,"Web Label","Radio Button",Bevel,Filebox,"Radio Group","Show All",13,_ShowSelectedControl_,True
Bevel1=Bevel1,1,12,128,8,414,287
TextBox1=TextBox,1,0,138,179,171,21,abc..
TextLabel1="Normal Text Label",1,1,138,18,103,20,8,Normal
TextLabel2="Bold Text Label",1,1,137,36,99,20,8,Bold
TextLabel3="Italic Text Label",1,1,137,53,94,18,8,Italic
TextLabel4="Underline Text Label",1,1,136,71,97,18,8,Underline
TextLabel5="Strike-Thru Text Label",1,1,136,89,106,18,8,Strike
NumberBox1=pNumberBox1,1,2,473,31,56,22,0,0,256,1,"__Increment positive number by a factor of 1"
NumberBox2=pNumberBox2,1,2,473,60,55,22,0,-256,256,2,"__Increment or decrement number by a factor of 2"
CheckBox1=CheckBox,1,3,137,110,104,20,False
ComboBox1="Option 1",1,4,136,134,115,21,"Option 1","Option 2","Option 3"
Image1=FAQ.gif,1,5,265,30,71,60,http://www.google.com,"__Search for more info"
TextFile1=TextFile.txt,1,6,135,209,175,76,
Button1=Button,1,8,361,27,98,25,pButton1,0,False
Button2="Image Button",1,8,360,66,99,25,pButton2,if_hammer_screwdriver_11945.bmp,False
Weblabel1="Search Google",1,10,264,103,69,18,http://www.google.com
RadioButton1=RadioButton1,1,11,324,124,100,20,True
RadioButton2=RadioButton2,1,11,324,144,100,20,False
RadioButton3=RadioButton3,1,11,324,164,100,20,False
FileBox1=,1,13,330,219,172,20,file
FileBox2=,1,13,330,262,172,20,dir
TextLabel6="Browse for File",1,1,331,202,179,18,12,Normal
TextLabel7="Browse For Directory",1,1,332,245,202,18,7,Normal
Bevel2=Bevel,1,12,250,19,104,82,8,Bold
RadioGroup1=RadioGroup,1,14,433,115,90,69,Option1,Option2,Option3,1

[InterfaceEncoded]
TextFile.txt=99,132
FAQ.gif=2066,2755
if_hammer_screwdriver_11945.bmp=643,858

[EncodedFile-InterfaceEncoded-TextFile.txt]
lines=0
0=eJzzSM3JyVcIzy/KSVHk5fIgiwcA61sVjnic4wlJrShxy8xJ1SupKGEYBSMNuEBpSRzyN1W/mTEwAQAtYwdJj9s6pwEAAAACAAAAJgAAABkAAAAAAAAAAQAAAAAAAAAAAAAA

[EncodedFile-InterfaceEncoded-FAQ.gif]
lines=0
0=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

[EncodedFile-InterfaceEncoded-if_hammer_screwdriver_11945.bmp]
lines=0
0=eJx1kktoWkEUhu0VUdJNKS66kYAbuxBcTJASgouSTdCatbh3E43iygohEAMxJLhwE3WjBtypJUoRfNUnKsbUB1hftAiJUJ8oig8Itwdve7lNyIEznPnnm+GfM/Px0wc6bR1CyPeQb/7mK9q7tY7B+tvXRP4LnU4Ho0QiKRQK1Wq13W73+/3xeDwajTqdTrPZLJVKBwcehDwXFwEcx9lstlarxTBMKpV2u13AZrPZYrGYz+eTyQT2Hh7eIHRjNOJbW1+AVyqVHA5HoVDQ6XS5XI7/H3r9d4S+npw87uxEj48rhKhWq7lcrkwmYzAYKpWKAlcQCur1q93du9PTX9RzwBKPxxOLxUwm02QyreEqQt80mvne3o+zs3v8WRgMBj6fLxKJWCzW0dE1QimFYiqR/Dw///0cJsLhcAgEgu1tG4Z9lsmG+/v3l5eDl2AivF7vxsY1dGNzM3B72yX1cDhsNBqhvU94i8VydRURCu80mirUhAhPAPBwOLRarVQYppFIBFzNZnMYk8mk2WwGEeBMJuN0OuPxOBVOpVIul4tU7HZ7sViMRqMwgg6vTy7ZbLZ8Pu92u0llOp16PJ5KpQKHAAn3InSfzwdwuVyGguoNPpLf72+1Wo1GI5vNwi7SxmAwCAQCVHi5XMZisVqt9vDwkEgkoIZPRSyl0+lgMAhmSLLX68Ht4OLQQzBfr9dBfKn/oVAIyFwuB57hu65WqycAjfYHnKBM43ick89Mi89IzM1NLYovTi5KLU8pyiwDsg0NLU1M9ZJyCxhGwbAGFswQWo0Ju7x+XK0RAxMAb7gNSCAe/30BAAAAAgAAADkAAAAmAgAAAAAAAAEAAAAAAAAAAAAAAA

```
