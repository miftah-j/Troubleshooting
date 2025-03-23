
## 📌 System & Performance Issues Topics:

🔹 Check system uptime:  
  
    wmic os get lastbootuptime  
  
🔹 View system logs for errors:  
  
    eventvwr.msc  

🔹 Scan and repair system files:  
 
    sfc /scannow 
 
🔹 Check for corrupted Windows files:  
  
    dism /online /cleanup-image /scanhealth  

🔹 Fix Windows Update issues:  
  
    net stop wuauserv  
    net stop bits  
    net start wuauserv  
    net start bits 
  
📌 Network Troubleshooting  
  
🔹 Check IP configuration:  
  
ipconfig /all  
  
🔹 Release and renew IP address:  
  
    ipconfig /release

    ipconfig /renew 
  
🔹 Test network latency:  
  
    ping 8.8.8.8 -t  

🔹 Trace network route:  
  
    tracert google.com

🔹 List active network connections:  
  
    netstat -ano

🔹 Find which process is using a port:  
  
    netstat -ano | find "80"  

## 📌 Disk & Storage Issues

  
🔹 Check disk for errors:  
  
    chkdsk C: /f /r 
  
🔹 Show detailed disk usage:  

    wmic logicaldisk get size,freespace,caption  
  
🔹 Check disk performance:  
  
    winsat disk  
 
🔹 List all partitions:  
  
    diskpart  

    list disk  

## 📌 User & Access Issues

  
🔹 Reset a local user password:  
  
    net user AdminUser NewPassword  
  
🔹 Find locked-out users in Active Directory:  
  
    net user /domain | find "Lockout"  
  
🔹 Force logout a user session remotely:  
  
    logoff /server:RemotePCName  
  
🔹 List all user sessions on a server:  
  
    qwinsta  

  
## 📌 Remote Management & Services

  
🔹 Check running services:  
  
    sc query state= all
  
🔹 Restart a service:  
  
    net stop spooler && net start spooler  
  
🔹 Enable RDP remotely:  
  
    reg add "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f  
  
🔹 Reboot a remote PC:  
  
    shutdown /r /m \\RemotePCName /t 0
