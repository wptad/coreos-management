# mount

## format

```
sudo parted /dev/sda --script mklabel gpt  mkpart primary ext4 0% 100% 

mkfs.ext4 -O ^has_journal -t ext4 -b 4096 /dev/sda1

```



## mount units

```
[Unit]
Description=data disk
Before=docker.service
[Mount]
What=/dev/sda1
Where=/hdd1
Type=ext4
Options=defaults

[Install]
WantedBy=multi-user.target

```

## bind units

*  var-lib-docker.mount 

```
[Unit]
Description=bind docker folder
Before=docker.service
After=hdd1.mount
[Mount]
What=/hdd1/docker
Where=/var/lib/docker
Type=none
Options=bind
[Install] 
WantedBy=multi-user.target
```

## write empty file

```
dd if=/dev/zero of=empty bs=1M count=8000
```
