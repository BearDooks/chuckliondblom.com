---
title: "Creating A Simple Menu In PowerShell"
date: 2015-10-29 20:26:26 -0500
categories: [guide]
tags: [GAM, google, google apps, menu, powershell]
author: chuck lindblom
sharing: true
show_author_profile: true
---

## Background:

I don&#8217;t claim to be the worlds best programmer, in fact I am far from it, but I do share something that all great programmers have. The love of simple code that is clean, and just works.

Recently I was working on a PowerShell project where I was trying to create a simple application that would ask the user for input, and then run an .exe int eh background with the passed data. The idea was to simply the program that we used to administer our Google Apps domain, called [GAM](https://github.com/jay0lee/GAM).

<figure>
	<a href="/images/powershell.png"><img src="images/powershell.png" alt=""></a>
</figure>

We had already been using the program for a while, but it was becoming annoying to type out the same commands all the time such as:
<!--more-->
<p style="padding-left: 30px;">
  gam user abc@abc.com delegate to user xyz@abc.com
</p>

I had two goals on this project:

  1. Ask the user for as little information as possible
  2. Draw up the code so it made sense, and the program would only stop when the user wanted it to

## Finished Product

{% highlight ruby %}

<pre>&lt;###################################################################### GAM Admin Written By Chuck Lindblom Changelog - C:\GAM\Changelog.txt All Code provided as is and used at your own risk. This is a work in progress!!! ######################################################################&gt;

$host.ui.RawUI.WindowTitle = "Conning GAM Admin Tool"

#############################
# - Check for client_secrets.json file
#############################
$xAppName    = "Conning_GAM_Admin_Menu"
[BOOLEAN]$global:xExitSession=$false
function LoadMenuSystem(){
	[INT]$MainMenu=0
	[INT]$SubMenu=0
	[BOOLEAN]$xValidSelection=$false
	while ( $MainMenu -lt 1 -or $MainMenu -gt 6 ){
		CLS

        #############################
		# - Present the Main Menu Options to the user
        #############################
		Write-Host "`n`tConning GAM Admin Menu - Version 0.4`n" -ForegroundColor Magenta
		Write-Host "`t`tPlease select an option`n" -Fore Cyan
		Write-Host "`t`t`t1. User Tasks" -Fore Cyan
		Write-Host "`t`t`t2. Group Tasks" -Fore Cyan
		Write-Host "`t`t`t3. Reports" -Fore Cyan
		Write-Host "`t`t`t4. Misc Tasks`n" -Fore Cyan
		Write-Host "`t`t`t5. Reload Tool (For Developing)" -Fore Red
		Write-Host "`t`t`t6. Quit and Exit`n" -Fore Yellow
		# -  Retrieve the response from the user
		[int]$MainMenu = Read-Host "`t`tEnter Menu Option Number"
		if( $MainMenu -lt 1 -or $MainMenu -gt 6 ){
			Write-Host "`tPlease select one of the options available.`n" -Fore Red;start-Sleep -Seconds 1
		}
	}
	Switch ($MainMenu){    # - User has selected a valid entry.. load Sub Menu

        #############################
		# - User Tasks Sub Menu
        #############################
		1 {
			while ( $SubMenu -lt 1 -or $SubMenu -gt 6 ){
				CLS
				# - Present the Sub Menu Options
				Write-Host "`n`tGAM Admin Menu - Version 0.3`n" -ForegroundColor Magenta
				Write-Host "`t`tPlease select the User administration task you require`n" -Fore Cyan
				Write-Host "`t`t`t1. Create New User" -Fore Cyan
				Write-Host "`t`t`t2. Get User Info" -Fore Cyan
				Write-Host "`t`t`t3. Show User Delegates" -Fore Cyan
				Write-Host "`t`t`t4. Create Email Delegate" -Fore Cyan
				Write-Host "`t`t`t5. Remove Email Delegate`n" -Fore Cyan
				Write-Host "`t`t`t6. Go to Main Menu`n" -Fore Yellow
				[int]$SubMenu = Read-Host "`t`tEnter Menu Option Number"
				if( $SubMenu -lt 1 -or $SubMenu -gt 6 ){
					Write-Host "`tPlease select one of the options available.`n" -Fore Red;start-Sleep -Seconds 1
				}
			}
			Switch ($SubMenu){
				1{ Write-Host "`n`tCreating New User`n" -Fore Yellow;Write-Host "`n`tWhat is the user's email address?`n" -Fore Yellow;$Email = [Console]::ReadLine();
				   Write-Host "`n`tWhat is the user's first name?`n" -Fore Yellow;$FN = [Console]::ReadLine();
				   Write-Host "`n`tWhat is the user's last name?`n" -Fore Yellow;$LN = [Console]::ReadLine();
				   Write-Host "`n`tDo you want to save the output? `n`t1. Yes `n`t2. No`n" -Fore Yellow;$Choice = [Console]::ReadLine(); Write-Host "`n";
				   while("1","2" -notcontains $Choice){
					Write-Host "`tError: Please select one of the options available`n`tDo you want to save the output? `n`t1. Yes `n`t2. No`n" -Fore Yellow;$Choice = [Console]::ReadLine(); Write-Host "`n";
				   }
                   if($Choice -eq 1){
                       C:\GAM\gam.exe create user $EMail firstname $FN lastname $LN password 'Conning2015';Write-Host "`n`tUser created with password: Conning2015`n" -Fore Yellow;C:\GAM\gam.exe create user $EMail firstname $FN lastname $LN password 'Conning2015' &gt;&gt; C:\GAM\Reports\CreateUser.txt;Write-Host "`n`tFile Saved To C:\GAM\Reports\CreateUser.txt`n" -Fore Yellow;
                   }
                   Else{
                       C:\GAM\gam.exe create user $EMail firstname $FN lastname $LN password 'Conning2015';Write-Host "`n`tUser created with password: Conning2015`n" -Fore Yellow;
                   }                    
                   Write-Host "Press any key to continue ...";$x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown") }
				2{ Write-Host "`n`tWhat is the user's email address?`n" -Fore Yellow;$Email = [Console]::ReadLine();
				   Write-Host "`n`tDo you want to save the output? `n`t1. Yes `n`t2. No`n" -Fore Yellow;$Choice = [Console]::ReadLine(); Write-Host "`n";
				   while("1","2" -notcontains $Choice){
					Write-Host "`tError: Please select one of the options available`n`tDo you want to save the output? `n`t1. Yes `n`t2. No`n" -Fore Yellow;$Choice = [Console]::ReadLine(); Write-Host "`n";
				   }
                   if($Choice -eq 1){
                       C:\GAM\gam.exe info user $Email;C:\GAM\gam.exe info user $Email &gt;&gt; C:\GAM\Reports\UserInfo.txt;Write-Host "`n`tFile Saved To C:\GAM\Reports\UserInfo.txt`n" -Fore Yellow;
                   }
                   Else{
                       C:\GAM\gam.exe info user $Email
                   }                    
                   Write-Host "Press any key to continue ...";$x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown") }
				3{ Write-Host "`n`tWhat is the email address?`n" -Fore Yellow;$Email = [Console]::ReadLine();
                   Write-Host "`n`tDo you want to save the output? `n`t1. Yes `n`t2. No`n" -Fore Yellow;$Choice = [Console]::ReadLine(); Write-Host "`n";
                   while("1","2" -notcontains $Choice){
					Write-Host "`tError: Please select one of the options available`n`tDo you want to save the output? `n`t1. Yes `n`t2. No`n" -Fore Yellow;$Choice = [Console]::ReadLine(); Write-Host "`n";
				   }
				   if($Choice -eq 1){
                       C:\GAM\gam.exe user $Email show delegate;C:\GAM\gam.exe user $Email show delegate &gt;&gt; C:\GAM\Reports\UserDelegate.txt;Write-Host "`n`tFile Saved To C:\GAM\Reports\UserDelegate.txt`n" -Fore Yellow;
                   }
                   Else{
                       C:\GAM\gam.exe user $Email show delegate
                   }
                   Write-Host "Press any key to continue ...";$x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown") }
				4{ Write-Host "`n`tWhich Email Is Being Delegated?`n" -Fore Yellow;$Email1 = [Console]::ReadLine();
				   Write-Host "`n`tWhich Email Is It Being Delegated To?`n" -Fore Yellow;$Email2 = [Console]::ReadLine();
				   Write-Host "`n`tDo you want to save the output? `n`t1. Yes `n`t2. No`n" -Fore Yellow;$Choice = [Console]::ReadLine(); Write-Host "`n";
                   while("1","2" -notcontains $Choice){
					Write-Host "`tError: Please select one of the options available`n`tDo you want to save the output? `n`t1. Yes `n`t2. No`n" -Fore Yellow;$Choice = [Console]::ReadLine(); Write-Host "`n";
				   }
				   if($Choice -eq 1){
                       C:\GAM\gam.exe user $Email1 delegate to $Email2;C:\GAM\gam.exe user $Email1 delegate to $Email2 &gt;&gt; C:\GAM\Reports\EmailDelegation.txt;Write-Host "`n`tFile Saved To C:\GAM\Reports\EmailDelegation.txt`n" -Fore Yellow;
                   }
                   Else{
                       C:\GAM\gam.exe user $Email1 delegate to $Email2
                   }
                   Write-Host "Press any key to continue ...";$x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown") }
				5{ Write-Host "`n`tWhich Email Is Being Delegated?`n" -Fore Yellow;$Email1 = [Console]::ReadLine();
				   Write-Host "`n`tWhich Email Is Being Removed?`n" -Fore Yellow;$Email2 = [Console]::ReadLine();
				   Write-Host "`n`tDo you want to save the output? `n`t1. Yes `n`t2. No`n" -Fore Yellow;$Choice = [Console]::ReadLine(); Write-Host "`n";
                   while("1","2" -notcontains $Choice){
					Write-Host "`tError: Please select one of the options available`n`tDo you want to save the output? `n`t1. Yes `n`t2. No`n" -Fore Yellow;$Choice = [Console]::ReadLine(); Write-Host "`n";
				   }
				   if($Choice -eq 1){
                       C:\GAM\gam.exe user $Email1 delete delegate $Email2;C:\GAM\gam.exe user $Email1 delete delegate $Email2 &gt;&gt; C:\GAM\Reports\RemoveDelegation.txt;Write-Host "`n`tFile Saved To C:\GAM\Reports\RemoveDelegation.txt`n" -Fore Yellow;
                   }
                   Else{
                       C:\GAM\gam.exe user $Email1 delete delegate $Email2
                   }
                   Write-Host "Press any key to continue ...";$x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown") }
				default { Write-Host "`n`tQuit the Administration Tasks`n" -Fore Yellow; break}
			}
		}

        #############################
		# - Group Tasks Sub Menu
        #############################
		2 {
			while ( $SubMenu -lt 1 -or $SubMenu -gt 4 ){
				CLS
				# Present the Sub Menu Options
				Write-Host "`n`tGAM Admin Menu - Version 0.3`n" -ForegroundColor Magenta
				Write-Host "`t`tPlease select the Group administration task you require`n" -Fore Cyan
				Write-Host "`t`t`t1. Create a New EMail Group" -Fore Cyan
				Write-Host "`t`t`t2. Add User To Group" -Fore Cyan
				Write-Host "`t`t`t3. Get Group Info`n" -Fore Cyan
				Write-Host "`t`t`t4. Go to Main Menu`n" -Fore Yellow
				[int]$SubMenu = Read-Host "`t`tEnter Menu Option Number"
			}
			if( $SubMenu -lt 1 -or $SubMenu -gt 4 ){
				Write-Host "`tPlease select one of the options available.`n" -Fore Red;start-Sleep -Seconds 1
			}
			Switch ($SubMenu){
				1{ Write-Host "`n`tCreating New Group`n" -Fore Yellow;Write-Host "`n`tWhat is the Group Name`n" -Fore Yellow;$GroupName = [Console]::ReadLine();
				   Write-Host "`n`tWhat is the Group Email`n" -Fore Yellow;$GroupEmail = [Console]::ReadLine();
				   Write-Host "`n`tWhat is the Group Description`n" -Fore Yellow;$GroupDescription = [Console]::ReadLine();
				   while("1","2" -notcontains $Choice){
					Write-Host "`tError: Please select one of the options available`n`tDo you want to save the output? `n`t1. Yes `n`t2. No`n" -Fore Yellow;$Choice = [Console]::ReadLine(); Write-Host "`n";
				   }
				   if($Choice -eq 1){
                       C:\GAM\gam.exe create group $GroupEmail;C:\GAM\gam.exe update group $GroupEmail name $GroupName description $GroupDescription;Write-Host "`n`tGroup has been created`n" -Fore Yellow;  &gt;&gt; C:\GAM\Reports\CreateGroup.txt;Write-Host "`n`tFile Saved To C:\GAM\Reports\CreateGroup.txt`n" -Fore Yellow;
                   }
                   Else{
                       C:\GAM\gam.exe create group $GroupEmail;C:\GAM\gam.exe update group $GroupEmail name $GroupName description $GroupDescription;Write-Host "`n`tGroup has been created`n" -Fore Yellow;
                   }
                   Write-Host "Press any key to continue ...";$x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown") }
				2{ Write-Host "`n`tAdding User To Group`n" -Fore Yellow;Write-Host "`n`tWhat is the Group Email`n" -Fore Yellow;$GroupEmail = [Console]::ReadLine();
				   Write-Host "`n`tWhat is the New User's Email`n" -Fore Yellow;$UserEmail = [Console]::ReadLine();
				   while("1","2" -notcontains $Choice){
					Write-Host "`tError: Please select one of the options available`n`tDo you want to save the output? `n`t1. Yes `n`t2. No`n" -Fore Yellow;$Choice = [Console]::ReadLine(); Write-Host "`n";
				   }
				   if($Choice -eq 1){
                       C:\GAM\gam.exe update group $GroupEmail add member $UserEmail;Write-Host "`n`tUser Has Been Added`n" -Fore Yellow ;C:\GAM\gam.exe update group $GroupEmail add member $UserEmail  &gt;&gt; C:\GAM\Reports\GroupUserAdd.txt;Write-Host "`n`tFile Saved To C:\GAM\Reports\GroupUserAdd.txt`n" -Fore Yellow;
                   }
                   Else{
                       C:\GAM\gam.exe update group $GroupEmail add member $UserEmail;Write-Host "`n`tUser Has Been Added`n" -Fore Yellow 
                   }
                   Write-Host "Press any key to continue ...";$x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown") }
				3{ Write-Host "`n`tGetting Group Info`n" -Fore Yellow;Write-Host "`n`tWhat is the Group Email`n" -Fore Yellow;$GroupEmail = [Console]::ReadLine();
				   while("1","2" -notcontains $Choice){
					Write-Host "`tError: Please select one of the options available`n`tDo you want to save the output? `n`t1. Yes `n`t2. No`n" -Fore Yellow;$Choice = [Console]::ReadLine(); Write-Host "`n";
				   }
				   if($Choice -eq 1){
                       C:\GAM\gam.exe info group $GroupEmail ;C:\GAM\gam.exe info group $GroupEmail  &gt;&gt; C:\GAM\Reports\GroupInfo.txt;Write-Host "`n`tFile Saved To C:\GAM\Reports\GroupInfo.txt`n" -Fore Yellow;
                   }
                   Else{
                       C:\GAM\gam.exe info group $GroupEmail
                   }
                   Write-Host "Press any key to continue ...";$x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown") }
				default { Write-Host "`n`tGo to Main Menu`n" -Fore Yellow; break}
			}
		}

        #############################
		# - Reports Sub menu
        #############################
		3 {
			while ( $SubMenu -lt 1 -or $SubMenu -gt 10 ){
				CLS
				# Present the Sub Menu Options
				Write-Host "`n`tGAM Admin Menu - Version 0.3`n" -ForegroundColor Magenta
				Write-Host "`t`tPlease select the misc administration task you require`n" -Fore Cyan
				Write-Host "`t`t`t1. Admin Report" -Fore Cyan
                Write-Host "`t`t`t2. Domain Report" -Fore Cyan
				Write-Host "`t`t`t3. Docs Report" -Fore Cyan
				Write-Host "`t`t`t4. User Report" -Fore Cyan
				Write-Host "`t`t`t5. Login Audit Report" -Fore Cyan
				Write-Host "`t`t`t6. Mobile Devices Report" -Fore Cyan
				Write-Host "`t`t`t7. Group Report" -Fore Cyan
				Write-Host "`t`t`t8. Calendar Resource Report" -Fore Cyan
				Write-Host "`t`t`t9. License Report`n" -Fore Cyan
				Write-Host "`t`t`t10. Go to Main Menu`n" -Fore Yellow
				[int]$SubMenu = Read-Host "`t`tEnter Menu Option Number"
			}
			if( $SubMenu -lt 1 -or $SubMenu -gt 10 ){
				Write-Host "`tPlease select one of the options available.`n" -Fore Red;start-Sleep -Seconds 1
			}
			Switch ($SubMenu){
				1{ Write-Host "`n`tRunning Admin Report... `n"      -Fore Yellow;C:\GAM\gam.exe report admin &gt;&gt; C:\GAM\Reports\AdminReport.csv;dir C:\GAM\Reports\AdminReport.csv      | Rename-Item -NewName {$_.BaseName+(Get-Date -f yyyy-MM-dd)+$_.Extension};C:\GAM\gam.exe report admin;Write-Host  "`n`tReport Saved Locally: C:\GAM\Reports\`n" -Fore Yellow;Write-Host "Press any key to continue ...";$x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown") }
				2{ Write-Host "`n`tRunning Domain Report...`n"      -Fore Yellow;C:\GAM\gam.exe report admin &gt;&gt; C:\GAM\Reports\DomainReport.csv;dir C:\GAM\Reports\DomainReport.csv    | Rename-Item -NewName {$_.BaseName+(Get-Date -f yyyy-MM-dd)+$_.Extension};C:\GAM\gam.exe report domain;Write-Host "`n`tReport Saved Locally: C:\GAM\Reports\`n" -Fore Yellow;Write-Host "Press any key to continue ...";$x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown") }
				3{ Write-Host "`n`tRunning Docs Report...  `n"      -Fore Yellow;C:\GAM\gam.exe report admin &gt;&gt; C:\GAM\Reports\DocsReport.csv;dir C:\GAM\Reports\DocsReport.csv        | Rename-Item -NewName {$_.BaseName+(Get-Date -f yyyy-MM-dd)+$_.Extension};C:\GAM\gam.exe report logins;Write-Host "`n`tReport Saved Locally: C:\GAM\Reports\`n" -Fore Yellow;Write-Host "Press any key to continue ...";$x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown") }
				4{ Write-Host "`n`tRunning Users Report... `n"      -Fore Yellow;C:\GAM\gam.exe report admin &gt;&gt; C:\GAM\Reports\UsersReport.csv;dir C:\GAM\Reports\UsersReport.csv      | Rename-Item -NewName {$_.BaseName+(Get-Date -f yyyy-MM-dd)+$_.Extension};C:\GAM\gam.exe report users;Write-Host  "`n`tReport Saved Locally: C:\GAM\Reports\`n" -Fore Yellow;Write-Host "Press any key to continue ...";$x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown") }
				5{ Write-Host "`n`tRunning Login Audit Report...`n" -Fore Yellow;C:\GAM\gam.exe report admin &gt;&gt; C:\GAM\Reports\LoginReport.csv;dir C:\GAM\Reports\LoginReport.csv      | Rename-Item -NewName {$_.BaseName+(Get-Date -f yyyy-MM-dd)+$_.Extension};C:\GAM\gam.exe report docs;Write-Host   "`n`tReport Saved Locally: C:\GAM\Reports\`n" -Fore Yellow;Write-Host "Press any key to continue ...";$x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown") }
				6{ Write-Host "`n`tRunning Mobile Devices Report...`n" -Fore Yellow;C:\GAM\gam.exe print mobile &gt;&gt; C:\GAM\Reports\MobileDeviceReport.csv;dir C:\GAM\Reports\MobileDeviceReport.csv      | Rename-Item -NewName {$_.BaseName+(Get-Date -f yyyy-MM-dd)+$_.Extension};C:\GAM\gam.exe print mobile;Write-Host   "`n`tReport Saved Locally: C:\GAM\Reports\`n" -Fore Yellow;Write-Host "Press any key to continue ...";$x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown") }
				7{ Write-Host "`n`tRunning Group Report...`n" -Fore Yellow;C:\GAM\gam.exe print groups &gt;&gt; C:\GAM\Reports\GroupsReport.csv;dir C:\GAM\Reports\GroupsReport.csv      | Rename-Item -NewName {$_.BaseName+(Get-Date -f yyyy-MM-dd)+$_.Extension};C:\GAM\gam.exe print groups;Write-Host   "`n`tReport Saved Locally: C:\GAM\Reports\`n" -Fore Yellow;Write-Host "Press any key to continue ...";$x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown") }
				8{ Write-Host "`n`tRunning Resource Report...`n" -Fore Yellow;C:\GAM\gam.exe print resources &gt;&gt; C:\GAM\Reports\ResourceReport.csv;dir C:\GAM\Reports\ResourceReport.csv      | Rename-Item -NewName {$_.BaseName+(Get-Date -f yyyy-MM-dd)+$_.Extension};C:\GAM\gam.exe print resources;Write-Host   "`n`tReport Saved Locally: C:\GAM\Reports\`n" -Fore Yellow;Write-Host "Press any key to continue ...";$x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown") }
				9{ Write-Host "`n`tRunning License Report...`n" -Fore Yellow;C:\GAM\gam.exe print licenses &gt;&gt; C:\GAM\Reports\LicenseReport.csv;dir C:\GAM\Reports\LicenseReport.csv      | Rename-Item -NewName {$_.BaseName+(Get-Date -f yyyy-MM-dd)+$_.Extension};C:\GAM\gam.exe print licenses;Write-Host   "`n`tReport Saved Locally: C:\GAM\Reports\`n" -Fore Yellow;Write-Host "Press any key to continue ...";$x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown") }
				default { Write-Host "`n`tQuit the Misc Tasks`n" -Fore Yellow; break}
			}
		  }
		
        #############################
        # - Misc Tasks Sub menu
		#############################
        4 {
			while ( $SubMenu -lt 1 -or $SubMenu -gt 2 ){
				CLS
				# Present the Sub Menu Options
				Write-Host "`n`tGAM Admin Menu - Version 0.3`n" -ForegroundColor Magenta
				Write-Host "`t`tPlease select the misc administration task you require" -Fore Cyan
				Write-Host "`t`t`t1. What Is`n" -Fore Cyan
				Write-Host "`t`t`t2. Go to Main Menu`n" -Fore Yellow
				[int]$SubMenu = Read-Host "`t`tEnter Menu Option Number"
			}
			if( $SubMenu -lt 1 -or $SubMenu -gt 2 ){
				Write-Host "`tPlease select one of the options available.`n" -Fore Red;start-Sleep -Seconds 1
			}
			Switch ($SubMenu){
				1{ Write-Host "`n`tDetermining What Is...`n" -Fore Yellow;Write-Host "`n`tWhat is the Email Address`n" -Fore Yellow;$Email = [Console]::ReadLine();
				   while("1","2" -notcontains $Choice){
					Write-Host "`tError: Please select one of the options available`n`tDo you want to save the output? `n`t1. Yes `n`t2. No`n" -Fore Yellow;$Choice = [Console]::ReadLine(); Write-Host "`n";
				   }
				   if($Choice -eq 1){
                       C:\GAM\gam.exe whatis $EMail ;C:\GAM\gam.exe whatis $EMail  &gt;&gt; C:\GAM\Reports\WhatIs.txt;Write-Host "`n`tFile Saved To C:\GAM\Reports\WhatIs.txt`n" -Fore Yellow;
                   }
                   Else{
                       C:\GAM\gam.exe whatis $EMail 
                   }
                   Write-Host "Press any key to continue ...";$x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown") }
                default { Write-Host "`n`tQuit the Misc Tasks`n" -Fore Yellow; break}
			}
		  }
		  
		#############################
        # - Developer Reload Tool
        #############################
        5{ .\GAMAdmin.ps1 }
		# - Break The Loop
		default { $global:xExitSession=$true;break }
	}
}

#############################
# - Program Quit
#############################
LoadMenuSystem
If ($xExitSession){
	exit-pssession
}

#############################
# - Reload Program If Not Done
#############################
else{
	.\GAMAdmin.ps1
}
}

</pre>
{% endhighlight %}
