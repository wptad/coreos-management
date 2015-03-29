# docker


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