# Login-Script
Login Script link to AD and computer



#Region ;**** Directives created by AutoIt3Wrapper_GUI ****
#AutoIt3Wrapper_outfile=loginscript.exe
#EndRegion ;**** Directives created by AutoIt3Wrapper_GUI ****
#include "adfunctions.AU3"
#include <Process.au3>


Sleep(5000)
Dim $usergroups
Dim $usergroupname = ""
Dim $tcFolder = ""
dim $a = ""

If $CmdLine[0] > 0 Then
	$usergroupname = $CmdLine[1]
Else
	$usergroups = StringSplit(_ADSamAccountNameToFQDN(@UserName), ",")
EndIf

;delete drive mapping
;DriveMapDel("Z:")
DriveMapDel("G:")
DriveMapDel("X:")
DriveMapAdd("P:","\\NSWNAS002\userdata\" & @UserName,1)
DriveMapAdd("Z:","\\CTDATA\home$\" & @UserName,1)


ProcessClose ( "tc.exe" )
Sleep(3000)
If $usergroupname = "Win7" Then
	$tcFolder = "IT Support"
	DriveMapDel("I:")
	DriveMapAdd("I:","\\nswnas001\nas-data\IT",1)

	If FileExists (@UserProfileDir & "\Desktop\traycommander-it.exe") Then

		FileDelete(@UserProfileDir & "\Desktop\traycommander-it.exe")
		Sleep(2000)
		FileCopy ("\\nswdc\NETLOGON\Traycommander\traycommander-it.exe" , @UserProfileDir & "\Desktop")

	Else
	FileCopy ("\\nswdc\NETLOGON\Traycommander\traycommander-it.exe" , @UserProfileDir & "\Desktop")
EndIf

Elseif $usergroupname = "Win7APS" then
	$tcFolder = "Asia-Pacific Services"

		If FileExists (@UserProfileDir & "\Desktop\traycommander-asiapacificservices.exe") Then
		FileDelete(@UserProfileDir & "\Desktop\traycommander-asiapacificservices.exe")
		Sleep(2000)
		FileCopy ("\\nswdc\NETLOGON\Traycommander\traycommander-asiapacificservices.exe" , @UserProfileDir & "\Desktop")
	Else
	FileCopy ("\\nswdc\NETLOGON\Traycommander\traycommander-asiapacificservices.exe" , @UserProfileDir & "\Desktop")
EndIf


	Elseif $usergroupname = "Win7CS" then
	;delete drive mapping
	DriveMapDel("G:")
	DriveMapDel("X:")
	;mapping drive z: drive for all users, g: drive for accounts and airdesk
	DriveMapAdd("G:","\\ctdata\Galileo Desktop",1)

	;Run("\\nswdc\NETLOGON\1PrinterScript\Department\CSDeptPrinters.bat")

	$tcFolder = "Customer Services"

	If FileExists (@UserProfileDir & "\Desktop\traycommander-cs.exe") Then
		FileDelete(@UserProfileDir & "\Desktop\traycommander-cs.exe")
		Sleep(2000)
		FileCopy ("\\nswdc\NETLOGON\Traycommander\traycommander-cs.exe" , @UserProfileDir & "\Desktop")
	Else
	FileCopy ("\\nswdc\NETLOGON\Traycommander\traycommander-cs.exe" , @UserProfileDir & "\Desktop")
EndIf

	Elseif $usergroupname = "Win7GSA" then
	;delete drive mapping
	DriveMapDel("G:")
	DriveMapDel("X:")
	;mapping drive z: drive for all users, g: drive for accounts and airdesk
	DriveMapAdd("G:","\\ctdata\Galileo Desktop",1)

	;Run("\\nswdc\NETLOGON\1PrinterScript\Department\CSDeptPrinters.bat")

	$tcFolder = "GSA"

	If FileExists (@UserProfileDir & "\Desktop\traycommander-gsa.exe") Then
		FileDelete(@UserProfileDir & "\Desktop\traycommander-gsa.exe")
		Sleep(2000)
		FileCopy ("\\nswdc\NETLOGON\Traycommander\traycommander-gsa.exe" , @UserProfileDir & "\Desktop")
	Else
	FileCopy ("\\nswdc\NETLOGON\Traycommander\traycommander-gsa.exe" , @UserProfileDir & "\Desktop")
EndIf


Elseif $usergroupname = "Win7Finance" then
	;delete drive mapping
	DriveMapDel("G:")
	DriveMapDel("F:")

	;mapping drive z: drive for all users, g: drive for accounts and airdesk
	DriveMapAdd("G:","\\ctdata\Galileo Desktop",1)
	DriveMapAdd("F:","\\ctdata\Accounts\FINANCE DOCS",1)
	$tcFolder = "Finance"

	If FileExists (@UserProfileDir & "\Desktop\traycommander-finance.exe") Then
		FileDelete(@UserProfileDir & "\Desktop\traycommander-finance.exe")
		Sleep(2000)
		FileCopy ("\\nswdc\NETLOGON\Traycommander\traycommander-finace.exe" , @UserProfileDir & "\Desktop")
	Else
	FileCopy ("\\nswdc\NETLOGON\Traycommander\traycommander-finance.exe" , @UserProfileDir & "\Desktop")
EndIf

Elseif $usergroupname = "Win7Marketing" then

	DriveMapDel("R:")
	DriveMapDel("N:")

	;mapping drive z: drive for all users, g: drive for accounts and airdesk
	DriveMapAdd("R:","\\ctdata\Marketing",0)
	DriveMapAdd("N:","\\nswnas001\nas-data\Marketing",0)

	$tcFolder = "Marketing"

	If FileExists (@UserProfileDir & "\Desktop\traycommander-marketing.exe") Then
		FileDelete(@UserProfileDir & "\Desktop\traycommander-marketing.exe")
		Sleep(2000)
		FileCopy ("\\nswdc\NETLOGON\Traycommander\traycommander-marketing.exe" , @UserProfileDir & "\Desktop")
	Else
	FileCopy ("\\nswdc\NETLOGON\Traycommander\traycommander-marketing.exe" , @UserProfileDir & "\Desktop")
EndIf

Elseif $usergroupname = "Win7Sales" then
	DriveMapDel("s:")
	;mapping drive z: drive for all users, g: drive for accounts and airdesk
	DriveMapAdd("S:","\\ctdata\Sales",0)

	$tcFolder = "Sales"

	If FileExists (@UserProfileDir & "\Desktop\traycommander-sales.exe") Then
		FileDelete(@UserProfileDir & "\Desktop\traycommander-sales.exe")
		Sleep(2000)
		FileCopy ("\\nswdc\NETLOGON\Traycommander\traycommander-sales.exe" , @UserProfileDir & "\Desktop")
	Else
	FileCopy ("\\nswdc\NETLOGON\Traycommander\traycommander-sales.exe" , @UserProfileDir & "\Desktop")
EndIf

Elseif $usergroupname = "Win7Accounts" then

	DriveMapDel("F:")

	;mapping drive z: drive for all users, g: drive for accounts and airdesk
	DriveMapAdd("F:","\\ctdata\Accounts",1)

	$tcFolder = "Accounts"

	If FileExists (@UserProfileDir & "\Desktop\traycommander-accounts.exe") Then
		FileDelete(@UserProfileDir & "\Desktop\traycommander-accounts.exe")
		Sleep(2000)
		FileCopy ("\\nswdc\NETLOGON\Traycommander\traycommander-accounts.exe" , @UserProfileDir & "\Desktop")
	Else
	FileCopy ("\\nswdc\NETLOGON\Traycommander\traycommander-accounts.exe" , @UserProfileDir & "\Desktop")
EndIf

Elseif $usergroupname = "Win7HR" then

DriveMapDel("H:")
DriveMapDel("Q:")

	;mapping drive z: drive for all users, g: drive for accounts and airdesk
	DriveMapAdd("H:","\\ctdata\root\DR_Human_Resources",1)
	;DriveMapAdd("Q:","\\nas\Human Resources_Archived",1)

	$tcFolder = "Human Resources"

	If FileExists (@UserProfileDir & "\Desktop\traycommander-hr.exe") Then
		FileDelete(@UserProfileDir & "\Desktop\traycommander-hr.exe")
		Sleep(2000)
		FileCopy ("\\nswdc\NETLOGON\Traycommander\traycommander-hr.exe" , @UserProfileDir & "\Desktop")
	Else
	FileCopy ("\\nswdc\NETLOGON\Traycommander\traycommander-hr.exe" , @UserProfileDir & "\Desktop")
EndIf

Else

EndIf


;synchronize time
RunWait( @ComSpec & " /c " & "NET TIME \\" & @LogonServer & " /SET /YES", @SystemDir, @SW_HIDE )

Sleep ( 3000 ) ;sleep three seconds

If FileExists (@UserProfileDir & "\AppData\Roaming\Tray Commander") Then

DirRemove (@UserProfileDir & "\AppData\Roaming\Tray Commander", 1)
Sleep(2000)
DirCreate (@UserProfileDir & "\AppData\Roaming\Tray Commander")
Else
DirCreate (@UserProfileDir & "\AppData\Roaming\Tray Commander")
EndIf


$trayCommanderPath = "\\nswdc\NETLOGON\Globus Dashboard\" & $tcFolder    ;___________________SOURCE
$a = @UserProfileDir & "\AppData\Roaming\Tray Commander\"  ;_________________DESTINATION
$blueCowPath = "\\nswdc\NETLOGON\BluecowBatch\"


Sleep (5000)


#cs

If FileExists ("C:\BlueCow\Bluecow1a.bat") Then



Else
;DirCreate("C:\BlueCow")


FileCopy($blueCowPath & "Bluecow1a.bat", "C:\BlueCow", 1)
FileCopy($blueCowPath & "Bluecow1b.bat", "C:\BlueCow", 1)
FileCopy($blueCowPath & "BluecowTrain.bat", "C:\BlueCow", 1)
FileCopy($blueCowPath & "fix.bat", "C:\BlueCow", 1)

EndIf

#ce



If FileExists(@UserProfileDir & "\Desktop\TC.exe") Then

Else

$FileName = "C:\Program Files (x86)\Tray Commander\TC.exe"
$LinkFileName = @DesktopDir & "\TC.exe"
$LinkFileName = @DesktopDir & "\TC.exe"
$WorkingDirectory = @DesktopDir
$Icon = ""
$IconNumber = 57
$Description = "This is the text editor that comes with Windows"
$State = @SW_SHOWMAXIMIZED ;Can also be @SW_SHOWNORMAL or @SW_SHOWMINNOACTIVE

FileCreateShortcut($FileName,$LinkFileName,$WorkingDirectory,"",$Description,$Icon,"",$IconNumber,$State)

EndIf


If FileExists($trayCommanderPath & "\Commands.cfg") Then

FileCopy($trayCommanderPath & "\Commands.cfg", $a, 1)

EndIf

If FileExists($trayCommanderPath & "\Settings.ini") Then

FileCopy($trayCommanderPath & "\Settings.ini", $a, 1)

EndIf



Sleep (7000)

Run("C:\Program Files (x86)\Tray Commander\TC.exe")

