#Coreos Update

### proxy Files

* /etc/systemd/system/update-engine.service.d/proxy.conf 

```
[Service]
Environment=ALL_PROXY=socks5://admin-proxy-server:8080
```
### update strategy

* /etc/coreos/update.conf 

``` 
GROUP=beta
REBOOT_STRATEGY=off
```

### Manually Check

```
update_engine_client -check_for_update
journalctl -fu update-engine

```

### log

```
journalctl -fu update-engine

```


REF <http://www.linuxidc.com/Linux/2015-04/116081.htm>
