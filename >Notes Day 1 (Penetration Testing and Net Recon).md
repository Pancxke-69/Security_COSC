# CTFD - http://10.50.20.30:8000
### Username
```
JOHU-503-M
```
### Password
```
z3rO0sdmpFsRyRR
```
### jumpbox
```
10.50.30.50
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
## Network Reconaissance
##### Example HTML Page
`http://10.50.24.160/webexample/htmldemo.html`
HTML Code:
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
OUTPUTS:
```
Authors:  ['Albert Einstein', 'J.K. Rowling', 'Albert Einstein', 'Jane Austen', 'Marilyn Monroe', 'Albert Einstein', u’Andr\xe9 Gide', 'Thomas A. Edison', 'Eleanor Roosevelt', 'Steve Martin']
```
#### Script Management
Scripts are stored in a subdirectory of the Nmap data directory by default:
`/usr/share/nmap/scripts`




























