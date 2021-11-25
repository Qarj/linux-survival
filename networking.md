# Check port reachable

```
nc -zv 127.0.0.1 80
.
Connection to 127.0.0.1 80 port [tcp/*] succeeded!
```

```
cat < /dev/tcp/127.0.0.1/8080
.
SSH-2.0-APACHE-SSHD-2.7.0
```
