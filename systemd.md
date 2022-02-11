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

# timer

## mysql-backup-full.service
```
[Unit]
Description=full backup for mysql-1
After=mysql-1.service
[Service]
Type=oneshot
ExecStartPre=-/bin/bash -c '/bin/mkdir -p /hdd1/mysql-backup/data'
ExecStartPre=-/bin/bash -c '/bin/mv /hdd1/mysql-backup/data /hdd1/mysql-backup/data-$$(date +%%Y%%m%%d-%%H%%M%%S)'
ExecStart=/bin/bash -c "/usr/bin/docker run --rm \
-v /hdd1/mysql:/var/lib/mysql \
-v /hdd1/mysql-backup/data:/backup \
perconalab/percona-xtrabackup xtrabackup --compress --backup --host= --port= --user= --password= --target-dir=/backup/base"

[Install]
WantedBy=multi-user.target
```
## mysql-backup-full.timer   
```
[Unit]
Description=full backup mysql every week

[Timer]
OnBootSec=200
RandomizedDelaySec=100
OnCalendar=Sun *-*-* 00:10:05
Persistent=true

[Install]
WantedBy=timers.target
```

```
systemctl enable --now mysql-backup-full.timer
systemctl enable --now mysql-backup-full.service
systemctl start mysql-backup-full.service
systemctl start mysql-backup-full.timer
systemctl list-timers --all
```

OnCalender values: 
```
minutely
hourly
daily
monthly
weekly
yearly
quarterly
semiannually
```

- [Calendar Usage](https://www.freedesktop.org/software/systemd/man/systemd.time.html)
- [Systemd 入门教程：实战篇](https://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-part-two.html)
- [Systemd 定时器教程](http://www.ruanyifeng.com/blog/2018/03/systemd-timer.html)
- [Systemd 定时器教程](https://www.cnblogs.com/chengkanghua/p/12708584.html)
- [Creating A Timer](https://linuxhint.com/cron_systemd_timer/)
- [Timers (简体中文)](https://wiki.archlinux.org/title/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Timers_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))
