<div align="center">

## Vary Simple IRC Client


</div>

### Description

A Vart Simple And Basic IRC Client To Help Beginners To Connect To A IRC Server. It Will Just Connect And Get Data. It Has Ident And Ping Reply.
 
### More Info
 
Add 2-Buttons 1-richtextbox 2-winsocks (1 named wsMain and 1 names wsIDENT) and 1-timmer(interval set to 10) Then Copy And Paste All The Code


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Ryan Roy](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/ryan-roy.md)
**Level**          |Beginner
**User Rating**    |4.8 (19 globes from 4 users)
**Compatibility**  |VB 6\.0
**Category**       |[Internet/ HTML](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/internet-html__1-34.md)
**World**          |[Visual Basic](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/visual-basic.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/ryan-roy-vary-simple-irc-client__1-45127/archive/master.zip)

### API Declarations

Dim IdentName As String


### Source Code

```
Private Sub Command1_Click()
'This Connects To The IRC Server And THe Port To Use
  wsMain.Connect "oslo.no.eu.undernet.org", 6667
End Sub
Private Sub Command2_Click()
'This Disconnects You From The Server
  wsMain.SendData "QUIT :Your Reason For Quiting"
  wsMain.Close 'Closes The Socket So Its Ready To Use Again
End Sub
Private Sub Form_Load()
'This Sets Your Ident Name And The Port To Listen On
  IdentName = "My_IDENT_Name" 'Your Ident Name
  wsIDENT.LocalPort = 113 'The Port To Listen On
  wsIDENT.Listen 'Tells Socket To Listen
End Sub
Private Sub Timer1_Timer()
'This Is The Timer For The Ident
  If wsIDENT.State <> 2 And wsIDENT.State <> 7 Then 'If Socket Is Not Listening Or Has A Open Connection
    wsIDENT.Close 'Closes The Socket
    wsIDENT.Listen 'Reset The Socket To Listen
  End If
End Sub
Private Sub wsIDENT_ConnectionRequest(ByVal requestID As Long)
'This Is For When The Server Trys To Get Your Ident
  wsIDENT.Close 'Closes The Socket
  wsIDENT.Accept requestID 'Accepts The Connection From The Server
  wsIDENT.SendData "113, 133:USERID:WIN32:" & IdentName 'Send Your Ident Info To The Server
End Sub
Private Sub wsMain_Connect()
'This Sends The Data You Need To Connect To A Server
  wsMain.SendData "User " & "your@email.com" & " " & wsMain.LocalHostName & " " & wsMain.RemoteHost & " :" & "Your Real Name" & vbCrLf
  wsMain.SendData "NICK " & "Your_Nick" & vbCrLf
End Sub
Private Sub wsMain_DataArrival(ByVal bytesTotal As Long)
'This Gets The Data From The Server And Puts It Into The TextBox
Dim Data As String
  wsMain.GetData Data 'Gets The Data
'This Sends The Pong Back To THe Server When U Get A Ping Msg
  If Left(Data, Len("PING")) = "PING" Then 'If The Data Has PING In It
    wsMain.SendData Replace(Data, "PING", "PONG") & vbCrLf 'Replaces The PING With A PONG And Sends The Rest Of THe Line Back To The Server
  End If
'This Puts All The Data In The TextBox So U Can Read It
  RichTextBox1.Text = RichTextBox1.Text & Data
End Sub
```

