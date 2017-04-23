# systemd

### Global Environment
config file will set default environment variables for all systemd units.
* `/etc/systemd/system.conf.d/10-default-env.conf`
```
[Manager]
DefaultEnvironment=DEFAULT_IPV4=192.168.10.51 
DefaultEnvironment="VAR1=word1 word2" VAR2=word3 "VAR3=word 5 6"
```
### User Environment
set environment variables for all users logged in Container Linux. 
* `/etc/profile.env`
```
export HTTP_PROXY=http://192.168.0.1:3128
```

### Show Environemnt
```
systemctl show-environment
```
### Reload Environment
```
systemctl   daemon-reexec 
```

* Refer [stemd-system.conf](https://www.freedesktop.org/software/systemd/man/systemd-system.conf.html)
* Refer [using environment variables in systemd units](https://coreos.com/os/docs/latest/using-environment-variables-in-systemd-units.html)
* [CHAPTER 6. MANAGING SERVICES WITH SYSTEMD](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/System_Administrators_Guide/chap-Managing_Services_with_systemd.html)
