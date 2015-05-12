#coreos pxe install

* good example: <https://github.com/GoogleCloudPlatform/kubernetes/blob/9e5c0e3b3b9ca777a27f85300bd7375cb2a9306e/docs/getting-started-guides/coreos/bare_metal_offline.md>


* TFTP TREE

```
root@PXE:/srv/tftp# tree 
.
├── coreos-installer
│   ├── coreos_production_pxe_image.cpio.gz
│   ├── coreos_production_pxe_image.cpio.gz.sig
│   ├── coreos_production_pxe.vmlinuz
│   └── coreos_production_pxe.vmlinuz.sig
├── pxelinux.0
└-─ pxelinux.cfg
    └── default

* pxelinux.0 can be downloaded from debian boot install's file.

```





* pxelinux.cfg/default

```
default coreos
prompt 1
timeout 15

display boot.msg

label coreos
  menu default
  kernel coreos-installer/coreos_production_pxe.vmlinuz
  append initrd=coreos-installer/coreos_production_pxe_image.cpio.gz cloud-config-url=http://192.168.0.1/pxe-cloud-config.yml console=tty1 coreos.autologin=tty1 sshkey="ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCzSMv2Zv9l.... wptad@tom.com"
```


* pxe-cloud-config.yml

```
coreos:
  units:
    - name: etcd.service
      command: start
    - name: fleet.service
      command: start
    - name: 00-eth0.network
      runtime: true
      content: |
        [Match]
        Name=en*

        [Network]
        Address=192.168.0.15/24
        Gateway=192.168.0.1
ssh_authorized_keys:
  - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCzSMv2Zv9lZtsd+YQCAdqr2zcCJCNP31tnxKvFquVokoVPljR5...

```


* /etc/dhcp/dhcpd.conf

```
default-lease-time 600;
max-lease-time 7200;

allow booting;
allow bootp;

subnet 192.168.0.0 netmask 255.255.255.0 {
    range dynamic-bootp 192.168.0.3 192.168.0.253;
    filename "pxelinux.0";
    option domain-name "yourdomain.com";
    option domain-name-servers 114.114.114.114;
    option routers 192.168.0.1;
}

```




* write to hard disk

```
sudo coreos-install -d /dev/sda -b 'http://10.10.16.218:8077'

```