### error creating overlay mount to 

```
cp /run/systemd/system/docker.service /etc/systemd/system/docker.service
vi /run/systemd/system/docker.service 
# 注释掉 #Environment=DOCKER_SELINUX=--selinux-enabled=true 
# 然后reload一下配置文件
systemctl daemon-reload 
# 重启docker 即可 
systemctl restart docker
```
