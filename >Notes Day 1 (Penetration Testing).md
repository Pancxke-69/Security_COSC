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
for i in {1..254}; do (ping -c 1 192.168.65.$i | grep "bytes from" &) ; done
```
Output:
64 bytes from 192.168.65.2: icmp_seq=1 ttl=64 time=1.95 ms
64 bytes from 192.168.65.1: icmp_seq=1 ttl=64 time=1.12 ms
64 bytes from 192.168.65.8: icmp_seq=1 ttl=64 time=1.58 ms
64 bytes from 192.168.65.10: icmp_seq=1 ttl=128 time=1.05 ms
64 bytes from 192.168.65.20: icmp_seq=1 ttl=64 time=0.016 ms
64 bytes from 192.168.65.30: icmp_seq=1 ttl=64 time=0.104 ms
