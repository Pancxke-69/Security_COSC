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
OUTPUT:
```
64 bytes from 192.168.28.1: icmp_seq=1 ttl=64 time=4.51 ms
64 bytes from 192.168.28.2: icmp_seq=1 ttl=63 time=5.68 ms
64 bytes from 192.168.28.3: icmp_seq=1 ttl=63 time=7.92 ms
64 bytes from 192.168.28.97: icmp_seq=1 ttl=64 time=0.090 ms
64 bytes from 192.168.28.98: icmp_seq=1 ttl=63 time=1.43 ms
64 bytes from 192.168.28.99: icmp_seq=1 ttl=63 time=1.45 ms
64 bytes from 192.168.28.100: icmp_seq=1 ttl=63 time=0.908 ms
64 bytes from 192.168.28.105: icmp_seq=1 ttl=63 time=0.767 ms
64 bytes from 192.168.28.111: icmp_seq=1 ttl=63 time=0.762 ms
64 bytes from 192.168.28.120: icmp_seq=1 ttl=63 time=0.851 ms
64 bytes from 192.168.28.129: icmp_seq=1 ttl=64 time=0.078 ms
64 bytes from 192.168.28.130: icmp_seq=1 ttl=63 time=1.22 ms
64 bytes from 192.168.28.131: icmp_seq=1 ttl=63 time=1.38 ms
```
# Tunnel Example
```
ssh -S /tmp/jump dummy -O forward -L1111:192.168.28.111:80 -L2222:192.168.28.100:80
```
# Nmap the Found IPS
```
proxychains nmap 192.168.28.1,2,3,97,98,99,100,105,111,120,129,130,131
```
OUTPUT:
```
Nmap scan report for 192.168.28.1
Host is up (0.00037s latency).
All 1000 scanned ports on 192.168.28.1 are closed

Nmap scan report for 192.168.28.2
Host is up (0.00048s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE
53/tcp open  domain

Nmap scan report for 192.168.28.3
Host is up (0.00050s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE
53/tcp open  domain

Nmap scan report for 192.168.28.97
Host is up (0.00037s latency).
All 1000 scanned ports on 192.168.28.97 are closed

Nmap scan report for 192.168.28.98
Host is up (0.00047s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE
53/tcp open  domain

Nmap scan report for 192.168.28.99
Host is up (0.00048s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE
53/tcp open  domain

Nmap scan report for 192.168.28.100
Host is up (0.00042s latency).
Not shown: 998 closed ports
PORT     STATE SERVICE
80/tcp   open  http
2222/tcp open  EtherNetIP-1

Nmap scan report for 192.168.28.105
Host is up (0.00056s latency).
Not shown: 997 closed ports
PORT     STATE SERVICE
21/tcp   open  ftp
23/tcp   open  telnet
2222/tcp open  EtherNetIP-1

Nmap scan report for 192.168.28.111
Host is up (0.00043s latency).
Not shown: 997 closed ports
PORT     STATE SERVICE
80/tcp   open  http
2222/tcp open  EtherNetIP-1
8080/tcp open  http-proxy

Nmap scan report for 192.168.28.120
Host is up (0.00043s latency).
Not shown: 999 closed ports
PORT     STATE SERVICE
4242/tcp open  vrml-multi-use

Nmap scan report for 192.168.28.129
Host is up (0.00037s latency).
All 1000 scanned ports on 192.168.28.129 are closed

Nmap scan report for 192.168.28.130
Host is up (0.00049s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE
53/tcp open  domain

Nmap scan report for 192.168.28.131
Host is up (0.00044s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE
53/tcp open  domain
```
# Master Socket Command
```
ssh -MS /tmp/t1 student@127.0.0.1 -p 4444
```
# Cancel a socket
```
ssh -S /tmp/jump dummy -O cancel <PORT>:<IP>:<PORT>
```














