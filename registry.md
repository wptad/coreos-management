# registry

## mirror config

* /etc/systemd/system/docker.service.d/50-insecure-registry.conf 

```
[Service]
Environment='DOCKER_OPTS=--insecure-registry="10.11.0.0/16" --registry-mirror=http://REGISTRY_MIRROR_COM'
```


## install


```
docker run -e STORAGE_PATH=/registry -v /hdd1/docker-registry -p 5000:5000 --name registry -d registry

```


* [Run a Local Registry Mirror](https://github.com/docker/docker/blob/master/docs/sources/articles/registry_mirror.md)




### Registry URL

```
https://docker.yunpro.cn/
```
It's `https`, not http


### usage



Configure your Docker daemons to use our registry mirror

You will need to pass the `--registry-mirror` option to your Docker daemon on startup:

```
docker --registry-mirror=https://docker.yunpro.cn -d

```
OR

 add the `--registry-mirror`options to the `DOCKER_OPTS` variable in `/etc/default/docker`.
