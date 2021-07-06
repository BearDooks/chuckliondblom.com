---
title: 'Simple Port Checking Tool &#8211; AutoIT'
date: 2016-06-13 15:53:07 -0500
categories: [guide]
tags: [autoit, ip, port check, tools, windows, auto it]
author: chuck lindblom
sharing: true
show_author_profile: true
---
Below you will find some code to make a simple port checking tool in AutoIT. The tools simply asks the user for what IP address or Hostname they want to check, and what port. It will then confirm your entry and show you the result.

<figure>
	<a href="/images/autoit_output.jpg"><img src="images/autoit_output.jpg" alt=""></a>
</figure>
<!--more-->
{% highlight ruby %}

> ; Script Function:
  
> ; Check if a port is open on a machine and report back to the user
> 
> #include <FileConstants.au3>
  
> #include <MsgBoxConstants.au3>

> #include <WinAPIFiles.au3>
> 
> ; Run port check
> 
> UserPort ()
  
> CheckPort()
> 
> Func UserPort ()
> 
> <p style="padding-left: 30px;">
>   ; Ask user for what Port and server they want<br /> Global $Server = InputBox(&#8220;Server Hostname / IP&#8221;, &#8220;What is the Hostname or the IP of the server?&#8221;, &#8220;127.0.0.1&#8221;, &#8220;&#8221;, &#8211; 1, -1, 0, 0)<br /> Global $Port = InputBox(&#8220;Port&#8221;, &#8220;What port would you like to check?&#8221;, &#8220;25&#8221;, &#8220;&#8221;, &#8211; 1, -1, 0, 0)
> </p>
> 
> <p style="padding-left: 30px;">
>   ; Display their answer<br /> MsgBox($MB_SYSTEMMODAL, &#8220;Responses:&#8221;, &#8220;I will check &#8221; & $Server & &#8220;:&#8221; & $Port)
> </p>
> 
> EndFunc
> 
> Func CheckPort ()
> 
> <p style="padding-left: 30px;">
>   TCPStartup() ; Start the TCP service.
> </p>
> 
> <p style="padding-left: 30px;">
>   ; Register OnAutoItExit to be called when the script is closed.<br /> OnAutoItExitRegister(&#8220;OnAutoItExit&#8221;)
> </p>
> 
> <p style="padding-left: 30px;">
>   ; Assign a Local variable the socket and connect to a Listening socket with the IP Address and Port specified.<br /> Local $iSocket = TCPConnect($Server, $Port)
> </p>
> 
> <p style="padding-left: 30px;">
>   ; If an error occurred display the error code and return False.<br /> If @error Then<br /> ; The server is probably offline/port is not opened on the server.<br /> Local $iError = @error<br /> MsgBox(BitOR($MB_SYSTEMMODAL, $MB_ICONHAND), &#8220;&#8221;, &#8220;Could not connect, Error code: &#8221; & $iError)<br /> Return False<br /> Else<br /> MsgBox($MB_SYSTEMMODAL, &#8220;&#8221;, &#8220;Connection successful&#8221;)<br /> EndIf
> </p>
> 
> <p style="padding-left: 30px;">
>   ; Close the socket.<br /> TCPCloseSocket($iSocket)
> </p>
> 
> EndFunc
  
> Func OnAutoItExit()
> 
> <p style="padding-left: 30px;">
>   TCPShutdown() ; Close the TCP service.
> </p>
> 
> EndFunc
  
> Exit

{% endhighlight %}
