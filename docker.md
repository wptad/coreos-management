# docker

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