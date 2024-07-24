# Windows
#### Scheduled Tasks and Services
* Write Permissions
* Non-Standard Locactions
* Unquoted Executable Paths
* Vulnerabilities in Executables
* Permissions to Run as `SYSTEM`
#### DEMO: Finding vulnerable Scheduled Tasks
##### DLL Stuff
* Can you rename the file?
* Can you write to the directory?
* Go to procmon:
  - filter by process name "Name of Process"
  - Filter result contains "NAME NOT FOUND"
  - filter path contains ".dll"
* MSFVENOM
  - `msfvenom -p windows/exec CMD='cmd.exe /c "whoami" > C:\users\student\desktop\whoami.txt' -f dll > SSPICLI.dll`
  - SCP the file over to the windows station
#### EXE Replacement
* Can you rename the file?
* Can you write to the directory?
* MSFVENOM
  - `msfvenom -p windows/exec CMD='cmd.exe /c "whoami" > C:\users\student\desktop\whoami.txt' -f exe > putty.exe`
* Drag and drop the payload
```
auditpol /get /category:*
auditpol /get /category:* | findstr /i "success failure"
```
#### Important Microsoft Event IDs
* 4624/4625 - Successful/failed login
* 4720 - Account created
* 4672 - Adminstrative User logged on
* 7045 - Service Created

# Linux
##### Resources
* [GTFOBins](https://gtfobins.github.io)
#### Insecure Permissions
* CRON
* World-Writable Files and Directories
* Dot '.' in PATH
  - Why should you consider it for privilege escalation?
  - What commands should you run?

#### Vulnerable Software and Services
#### Unpatched Kernel Vulnerabilities
## Persistence
* Adding vs hijacking a user account
* User account considerations?
* How should you access it?
#### User Account Demo
```

```
### Boot Process Persistence Demo
```

```
### Cron Persistence Demo
```

```
### Kernel Module Persistence Demo
```

```

















