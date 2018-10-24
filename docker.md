# docker

## docker service in coreos


```
cat /etc/systemd/system/docker.service 
[Unit]
Requires=torcx.target
After=torcx.target
Description=Docker Application Container Engine
Documentation=http://docs.docker.com
After=containerd.service docker.socket network-online.target
Wants=network-online.target
Requires=containerd.service docker.socket

[Service]
EnvironmentFile=/run/metadata/torcx
Environment=TORCX_IMAGEDIR=/docker
Type=notify
EnvironmentFile=-/run/flannel/flannel_docker_opts.env
Environment=DOCKER_STORAGE_OPTIONS="--storage-driver overlay"


# the default is not to use systemd for cgroups because the delegate issues still
# exists and systemd currently does not support the cgroup feature set required
# for containers run by docker
ExecStart=/usr/bin/env PATH=${TORCX_BINDIR}:${PATH} ${TORCX_BINDIR}/dockerd --host=fd:// --containerd=/var/run/docker/libcontainerd/docker-containerd.sock $DOCKER_SELINUX $DOCKER_OPTS $DOCKER_CGROUPS $DOCKER_OPT_BIP $DOCKER_OPT_MTU $DOCKER_OPT_IPMASQ
ExecReload=/bin/kill -s HUP $MAINPID
LimitNOFILE=1048576
# Having non-zero Limit*s causes performance problems due to accounting overhead
# in the kernel. We recommend using cgroups to do container-local accounting.
LimitNPROC=infinity
LimitCORE=infinity
# Uncomment TasksMax if your systemd version supports it.
# Only systemd 226 and above support this version.
TasksMax=infinity
TimeoutStartSec=0
# set delegate yes so that systemd does not reset the cgroups of docker containers
Delegate=yes
# kill only the docker process, not all processes in the cgroup
KillMode=process
# restart the docker process if it exits prematurely
Restart=on-failure
StartLimitBurst=3
StartLimitInterval=60s

[Install]
WantedBy=multi-user.target
```

## how to fix aliyun storage problem
* from https://github.com/coreos/bugs/issues/2340

```
# fix wrong driver
echo '{ "storage-driver": "devicemapper" }' | sudo tee /etc/docker/daemon.json
sudo systemctl restart docker.service

# fix aliyun buggy selinux
sudo sed -i 's/SELINUXTYPE=mcs/SELINUXTYPE=targeted/' /etc/selinux/config


```

## env-file

* /etc/systemd/system/example.service

```
[Unit]
Description=example
After=docker.service
Requires=docker.service
[Service]
TimeoutStartSec=0
ExecStartPre=-/usr/bin/docker rm example
ExecStart=/usr/bin/docker run \
    --name example \
    --env-file /data/project/production.env \
    -v /etc/localtime:/etc/localtime:ro \
    --log-driver=none \
    example/example:latest
ExecStop=/usr/bin/docker kill example
Restart=always
RestartSec=5
[Install]
WantedBy=multi-user.target
```

## run docker

```

docker run -e STORAGE_PATH=/registry -v /hdd1/docker-registry/:/registry -p 80:5000 -e STANDALONE=false -e MIRROR_SOURCE=https://registry-1.docker.io -e MIRROR_SOURCE_INDEX=https://index.docker.io --name registry -d registry


docker run -v /home/core/dockerfiles/adpro/nodejs-ad-server/nodejs-ad-server/:/project -v /home/core/.ssh/:/root/.ssh --rm -it -w /project node /bin/bash




```


## clear all container file and mirror files

```
  docker kill $(docker ps -q) ; docker rm $(docker ps -a -q) ; docker rmi $(docker images -q -a) 

```



## docker default OPT

```
/etc/systemd/system/docker.service.d/50-insecure-registry.conf
    content: |
        [Service]
        Environment='DOCKER_OPTS=--insecure-registry="10.11.0.0/16" --registry-mirror=http://docker.yunpro.cn'
        
```
