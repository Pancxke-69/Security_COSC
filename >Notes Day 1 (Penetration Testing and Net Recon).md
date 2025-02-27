# CTFD - http://10.50.20.30:8000
### Username
```
JOHU-503-M
```
### jumpbox
```
10.50.30.50
```
#### Password
```
z3rO0sdmpFsRyRR
```
### Lin-Ops
```
10.50.30.231
```
### WIN-OPS
```
10.50.38.121
```
#### XFREERDP COMMAND
```
xfreerdp /u:student /v:10.50.38.121 -dynamic-resolution +glyph-cache +clipboard
```
#### Password
```
password
```
### Stack Number - 13
### Multiplexing command
```
ssh -MS /tmp/jump student@10.50.30.50
```
* Multiplexing allows us to connect to multiple hosts using the same ssh
* Stays persistent until connection closes
### Dynamic port forwarding on a socket
```
ssh -S /tmp/jump dummy -O forward -D9050
```
* -O is for general options
### Ruby Ping Sweep
```
for i in {1..254}; do (ping -c 1 192.168.28.$i | grep "bytes from" &) ; done
```

### Cancel a socket
```
ssh -S /tmp/jump dummy -O cancel <PORT>:<IP>:<PORT>
```
### Example Commands
```
ssh -MS /tmp/jump student@10.50.39.25
ssh -S /tmp/jump dummy -O forward -D9050
for i in {1..254}; do (ping -c 1 192.168.28.$i | grep "bytes from" &) ; done
proxychains nmap 192.168.28.1,2,3,97,98,99,100,105,111,120,129,130,131
proxychains nc 192.168.28.111 80
proxychains nc 192.168.29.100 80
ssh -S /tmp/jump dummy -O forward -L1111:192.168.111:80 -L2222:192.168.28.100
firefox 127.0.0.1:1111
ssh -S /tmp/jump dummy -O forward -L1111:192.168.111:80 -L2222:192.168.28.100 -L4444:192.168.28.111:22
ssh -MS /tmp/t1 student@127.0.0.1 -p 4444
ssh -S /tmp/t1 dummy -O forward -L5555:192.168.50.100:22
ssh -MS /tmp/t2 credentials@127.0.0.1 -p 5555
```
# Lecture

## Pen-Testing
#### Penetration testing overview
* Phase 1: Mission Definition
* Phase 2: Recon
* Phase 3: Footprinting
* Phase 4: Exmploitation/Initial Access
* Phase 5: Post-Exploitation
* Phase 6: Document Mission
#### Write a formal report
* Opnotes
* Formalized Report
  - Executive Summary
  - Technical Summary
* Operational Concerns
  - Offensive
  - Defensive

 
## Reconaissance
##### Example HTML Page - http://10.50.24.160/webexample/htmldemo.html
HTML Code from above link:
```
<!DOCTYPE html>
<html>
<head>
<title>Page Title </title>
</head>
<body>
<h1>This is a Heading, we can use h6, but makes items smaller</h1>
<h6>See its smaller</h6>
<p>This is a paragraph.</p>
<p>Paragraph with 2 lines <br>
this is the other line
</p>
<img src="shutterstock_246695119_1080.jpg" height="500" width="500"> <br>
<button type="button">Make a button, this one does nothing
<! Notice anything wrong with the button?  Oh and this is a comment>
</body>
</html>
```
#### Scraping Data
`pip install lxml requests`
```
#!/usr/bin/python
import lxml.html
import requests

page = requests.get('http://quotes.toscrape.com')
tree = lxml.html.fromstring(page.content)

authors = tree.xpath('//small[@class="author"]/text()')

print ('Authors: ',authors)
```
* Things to change in the script
  - URL
  - xpath query
###### OUTPUTS:
```
Authors:  ['Albert Einstein', 'J.K. Rowling', 'Albert Einstein', 'Jane Austen', 'Marilyn Monroe', 'Albert Einstein', u’Andr\xe9 Gide', 'Thomas A. Edison', 'Eleanor Roosevelt', 'Steve Martin']
```
#### Script Management
Scripts are stored in a subdirectory of the Nmap data directory by default: `/usr/share/nmap/scripts`
```
nmap --script=http-enum 192.168.28.100
```
* Enumerates the directories and files on a web server


# CTF Notes
## Reconaissance
* Network scan `192.168.28.96/27`
* Network scan `192.168.150.224/27`
* Known URL: `consulting.site.donavia`



## Exploit and Research
### OUTPUT FROM RUBY PING SWEEP:
```
64 bytes from 192.168.28.97: icmp_seq=1 ttl=64 time=6.51 ms
64 bytes from 192.168.28.100: icmp_seq=1 ttl=63 time=2.83 ms
64 bytes from 192.168.28.98: icmp_seq=1 ttl=63 time=5.92 ms
64 bytes from 192.168.28.99: icmp_seq=1 ttl=63 time=4.69 ms
64 bytes from 192.168.28.105: icmp_seq=1 ttl=63 time=0.430 ms
64 bytes from 192.168.28.111: icmp_seq=1 ttl=63 time=0.721 ms
64 bytes from 192.168.28.120: icmp_seq=1 ttl=63 time=0.431 ms
```
#### NMAP Command filters on port 21
```
proxychains nmap 192.168.28.97,100,98,99,105,111,120 -p 21 --open 2>/dev/null
```
```192.168.28.105 has ftp open

PORT     STATE SERVICE
21/tcp   open  ftp
23/tcp   open  telnet
2222/tcp open  EtherNetIP-1


for i in {225..254}; do (ping -c 1 192.168.150.$i | grep "bytes from" &) ; done
64 bytes from 192.168.150.225: icmp_seq=1 ttl=64 time=0.811 ms
64 bytes from 192.168.150.226: icmp_seq=1 ttl=63 time=1.68 ms
64 bytes from 192.168.150.227: icmp_seq=1 ttl=63 time=2.31 ms


proxychains nmap -T4 192.168.28.97,100,98,99,105,111,120 -p80 --open

Nmap scan report for 192.168.28.100
Host is up (0.0015s latency).

PORT   STATE SERVICE
80/tcp open  http

Nmap scan report for 192.168.28.111
Host is up (0.00100s latency).

PORT   STATE SERVICE
80/tcp open  http
```
# Tunnels Tunnels and Tunnels
* `ssh -MS /tmp/jump student@<JUMP>`
  - This makes a tunnel named jump and stores it in /tmp
* `ssh -S /tmp/jump jump -O forward -D9050`
  - This adds an option to the Tunnel "jump" ( The option is proxchains )
* `ssh -S /tmp/jump jump -O forward -L 1111:<IP>:80`
  - This adds a port forward to an IP at port 80 naming it the port 1111
* `ssh -MS /tmp/t1 billybob@127.0.0.1`
  - This creates a new tunnel using the port forward that was created with the tunnel "jump"

# Tunnel Example

```
LINOPS		JUMP		T1		T2		T3
```


* `TERMINAL_1>/> ssh -MS /tmp/jump student@<jump_IP>`
* Creates Tunnel to jump box

* `<TERMINAL_2>/> ssh -S /tmp/jump skibidi -O forward -D9050`
* Creates Dynamic Tunnel (PROXYCHAINS) on the jump box
* `<TERMINAL_2>/> ssh -S /tmp/jump skibidi -O cancel -D9050`
* Cancels proxychains on the jump box
* `<TERMINAL_2>/> ssh -S /tmp/jump skibidi -O forward -L 1111:<T1>:2222`
* Creates a forward to "T1" IP on alternate port 2222
* `<TERMINAL_2>/> firefox 127.0.0.1:1111`
* Opens website from the "T1" box with firefox
* `<TERMINAL_2>/> ssh -MS /tmp/t1 student@<127.0.0.1> -p 1111`
* Creates a New tunnel using the loopback and connects to the port forward that we made above

* `<TERMINAL_3>/> ssh -S /tmp/t1 stupid -O forward -D9050`
* Creates proxychains on t1
* `<TERMINAL_3>/> ssh -S /tmp/t1 stupid -O cancel -D9050`
* Cancels proxychains on t1
* `<TERMINAL_3>/> ssh -S /tmp/t1 skibidi -O forward -L 5678:<T2>2222`
* Creates a forward to "t2" IP on alternate port 2222
* `<TERMINAL_3>/> ssh -MS /tmp/t2 student@<127.0.0.1> -p 5678`
* Creates a new tunnel using the loopback and connects to the port forward that we made above

* `<TERMINAL_4>/> ssh -S /tmp/t2 dumb -O forward -D9050`
* Creates proxychains on t2
* `<TERMINAL_4>/> ssh -S /tmp/t2 dumb -O forward -L 1234:<t3_IP>:21 `
* Creates forward to t3 on port 21















