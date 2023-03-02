### how to change default ssh port for coreos

```
cat > /etc/systemd/system/sshd.socket <<-EOF
[Unit]
Description=OpenSSH Server Socket
Conflicts=sshd.service

[Socket]
ListenStream=2222
Accept=yes

[Install]
WantedBy=sockets.target
EOF


systemctl restart sshd.socket

```



```
sudo vi /etc/ssh/sshd_config

Port 2222
```
