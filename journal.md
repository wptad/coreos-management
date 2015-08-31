#journal


## system log

```
journalctl --system

```

## sshd log

```
journalctl _COMM=sshd

```

## coreos cloudinit log

```
journalctl _EXE=/usr/bin/coreos-cloudinit
```


## REF

* <https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/System_Administrators_Guide/s1-Using_the_Journal.html>