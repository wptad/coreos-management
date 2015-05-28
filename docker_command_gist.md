## Docker command gist

### login into container 

```
docker run --rm  -it mongo /bin/bash

```

### run mongodb

```
docker run --name standalone-mongo -p 1251:27017 -v /hdd1/standalone_mongo:/data/db -d mongo 

```
#### mongo rs example

```
docker run \
  --name mongo_rs1 \
  -p 1301:27017 \
  -v /hdd1/mongo_rs1:/data/db \
  -d mongo \
  --replSet rs1 
  
```


### docker private registry
  
```
docker run -e STORAGE_PATH=/registry -v /hdd1/private-registry -p 8001:5000 --name private-registry -d registry

```

### docker public mirror

```

docker run -e STORAGE_PATH=/registry -v /hdd1/mirror-registry/:/registry -p 80:5000 -e STANDALONE=false -e MIRROR_SOURCE=https://registry-1.docker.io -e MIRROR_SOURCE_INDEX=https://index.docker.io --name mirror-registry -d registry
```


### how use sshfs to mount inside docker

```
--cap-add SYS_ADMIN --device /dev/fuse
```

* <https://github.com/docker/docker/issues/9448>