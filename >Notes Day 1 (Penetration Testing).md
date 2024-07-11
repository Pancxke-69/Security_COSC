# Username
```
JOHU-503-M
```
# Password
```
z3rO0sdmpFsRyRR
```
# jumpbox
```
10.50.30.50
```
# CTFD - http://10.50.20.30:8000
# Stack Number - 13
# Multiplexing command
```
ssh -MS /tmp/jump student@10.50.30.50
```
* Multiplexing allows us to connect to multiple hosts using the same ssh
# Dynamic port forwarding on a socket
```
ssh -S /tmp/jump dummy -O forward -D9050
```
