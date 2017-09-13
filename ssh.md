### how to change default ssh port for coreos

```
cat > /etc/systemd/system/sshd.socket <<-EOF
[Unit]
Description=OpenSSH Server Socket
Conflicts=sshd.service

[Socket]
ListenStream=54321
Accept=yes

[Install]
WantedBy=sockets.target
EOF


systemctl restart sshd.socket

```
