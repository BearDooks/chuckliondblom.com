---
title: "SMTP Tester Powershell"
date: 2016-06-13 16:17:04 -0500
categories: [guide]
tags: [email, powershell, program, smtp, windows]
author: chuck lindblom
sharing: true
show_author_profile: true
---

The below script is a simple method to test if port 25 is open on a server. The script will attempt to connect to the server and send a quick email with a small attachment that it creates on the fly.

<figure>
	<a href="/images/mail_icon.png"><img src="images/mail_icon.png" alt=""></a>
</figure>
<!--more-->
{% highlight ruby %}

<pre class="brush: powershell; title: ; notranslate" title="">######################################################################
# - Company SMTP Tester Tool
######################################################################

$host.ui.RawUI.WindowTitle = "Company SMTP Tester Tool"

$xAppName&nbsp;&nbsp;&nbsp; = "Company_SMTP_Tester_Tool"
[BOOLEAN]$global:xExitSession=$false
function LoadMenuSystem(){
[INT]$MainMenu=0
[INT]$SubMenu=0
[BOOLEAN]$xValidSelection=$false
while ( $MainMenu -lt 1 -or $MainMenu -gt 5 ){
CLS

#############################
# - Present the Main Menu Options to the user
#############################
Write-Host "`n`tCompany SMTP Tester Tool - Version 1.0`n" -ForegroundColor Magenta
Write-Host "`t`tPlease select a location`n" -Fore Cyan
Write-Host "`t`t`t1. Test SMTP" -Fore Cyan
Write-Host "`t`t`t2. Colo SMTP" -Fore Cyan
Write-Host "`t`t`t3. London SMTP" -Fore Cyan
Write-Host "`t`t`t4. Load Balancer`n" -Fore Cyan
Write-Host "`t`t`t5. Quit and Exit`n" -Fore Yellow
# -&nbsp; Retrieve the response from the user
[int]$MainMenu = Read-Host "`t`tEnter Location Number"
if( $MainMenu -lt 1 -or $MainMenu -gt 5 ){
Write-Host "`tPlease select one of the avialble locations.`n" -Fore Red;start-Sleep -Seconds 1
}
}
Switch ($MainMenu){

#############################
# - Test SMTP
#############################
1 {
#############################
# - Set correct SMTP Server to test with
#############################

$PSEmailServer = "127.0.0.1"

#############################
# - Create temp file to send
#############################

$tempFile = [System.IO.Path]::GetTempFileName()

#############################
# - Ask for the Sender and Reciver of the email
#############################

Write-Host "`n`nWhat is the sending email address?`n" -Fore Yellow;
$sendingemail = [Console]::ReadLine();

Write-Host "`nWho will recieve this email?`n" -Fore Yellow;
$recieveemail = [Console]::ReadLine();

#############################
# - Send the email based on user input and kill temp file
#############################

Send-MailMessage -From "$sendingemail" -To "$recieveemail" -Subject "Test email from Company" -Body "This is a test email from Company IT Support, Please ignore this." -Attachments "$tempFile" -dno onSuccess, onFailure -smtpServer $PSEmailServer
Remove-Item -Force $tempFile

#############################
# - Let the user know you sent the email
#############################

Write-Host "`n`nAn email has been sent from $sendingemail to $recieveemail`n" -Fore Yellow;
Write-Host "Press any key to continue ..."

$x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown")
}

#############################
# - Colo SMTP
#############################
2 {
#############################
# - Set correct SMTP Server to test with
#############################

$PSEmailServer = "127.0.0.1"

#############################
# - Create temp file to send
#############################

$tempFile = [System.IO.Path]::GetTempFileName()

#############################
# - Ask for the Sender and Reciver of the email
#############################

Write-Host "`n`nWhat is the sending email address?`n" -Fore Yellow;
$sendingemail = [Console]::ReadLine();

Write-Host "`nWho will recieve this email?`n" -Fore Yellow;
$recieveemail = [Console]::ReadLine();

#############################
# - Send the email based on user input and kill temp file
#############################

Send-MailMessage -From "$sendingemail" -To "$recieveemail" -Subject "Test email from Company" -Body "This is a test email from Company IT Support, Please ignore this." -Attachments "$tempFile" -dno onSuccess, onFailure -smtpServer $PSEmailServer
Remove-Item -Force $tempFile

#############################
# - Let the user know you sent the email
#############################

Write-Host "`n`nAn email has been sent from $sendingemail to $recieveemail`n" -Fore Yellow;
Write-Host "Press any key to continue ..."

$x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown")
}

#############################
# - London SMTP
#############################
3 {
#############################
# - Set correct SMTP Server to test with
#############################

$PSEmailServer = "127.0.0.1"

#############################
# - Create temp file to send
#############################

$tempFile = [System.IO.Path]::GetTempFileName()

#############################
# - Ask for the Sender and Reciver of the email
#############################

Write-Host "`n`nWhat is the sending email address?`n" -Fore Yellow;
$sendingemail = [Console]::ReadLine();

Write-Host "`nWho will recieve this email?`n" -Fore Yellow;
$recieveemail = [Console]::ReadLine();

#############################
# - Send the email based on user input and kill temp file
#############################

Send-MailMessage -From "$sendingemail" -To "$recieveemail" -Subject "Test email from Company" -Body "This is a test email from Company IT Support, Please ignore this." -Attachments "$tempFile" -dno onSuccess, onFailure -smtpServer $PSEmailServer
Remove-Item -Force $tempFile

#############################
# - Let the user know you sent the email
#############################

Write-Host "`n`nAn email has been sent from $sendingemail to $recieveemail`n" -Fore Yellow;
Write-Host "Press any key to continue ..."

$x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown")
}

#############################
# - Load Balancer
#############################
4 {
#############################
# - Set correct SMTP Server to test with
#############################

$PSEmailServer = "127.0.01"

#############################
# - Create temp file to send
#############################

$tempFile = [System.IO.Path]::GetTempFileName()

#############################
# - Ask for the Sender and Reciver of the email
#############################

Write-Host "`n`nWhat is the sending email address?`n" -Fore Yellow;
$sendingemail = [Console]::ReadLine();

Write-Host "`nWho will recieve this email?`n" -Fore Yellow;
$recieveemail = [Console]::ReadLine();

#############################
# - Send the email based on user input and kill temp file
#############################

Send-MailMessage -From "$sendingemail" -To "$recieveemail" -Subject "Test email from Company" -Body "This is a test email from Company IT Support, Please ignore this." -Attachments "$tempFile" -dno onSuccess, onFailure -smtpServer $PSEmailServer
Remove-Item -Force $tempFile

#############################
# - Let the user know you sent the email
#############################

Write-Host "`n`nAn email has been sent from $sendingemail to $recieveemail`n" -Fore Yellow;
Write-Host "Press any key to continue ..."

$x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown")
}
# - Break The Loop
default { $global:xExitSession=$true;break }
}
}

LoadMenuSystem
If ($xExitSession){
exit-pssession&nbsp;&nbsp;&nbsp; # - Quit Program
}else{
.\SMTPTester.ps1&nbsp;&nbsp;&nbsp; # - Loop To Top
}
</pre>
{% endhighlight %}
