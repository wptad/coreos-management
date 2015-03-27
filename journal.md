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