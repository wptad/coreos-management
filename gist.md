#gist

```
CoreOS 实战：剖析 etcd: <http://www.infoq.com/cn/articles/coreos-analyse-etcd/>


Coreos 安装及配置

http://ju.outofmemory.cn/entry/112616


安装之后如果发现有问题并且进不去系统,比如网络故障，可以用 Live CD 来修复,将有 问题的系统挂在到Live CD上修改user_data即可。 命令如下 :

 mount -o subvol=root /dev/sda9 /mnt/
 
```



# Error from server: no kind "Service" is registered for version "v1beta1"


```

$ etcdctl get /registry/namespaces/default
{"kind":"Namespace","id":"default","uid":"8b05a41a-c633-11e4-be1c-fa163e837eb3","creationTimestamp":"2015-03-09T08:09:00Z","apiVersion":"v1beta1","spec":{},"status":{}}
$ etcdctl rm --recursive /registry
$ etcdctl get /registry/namespaces/default
{"kind":"Namespace","apiVersion":"v1","metadata":{"name":"default","uid":"530e001a-1329-11e5-a04e-fa163e837eb3","creationTimestamp":"2015-06-15T06:39:51Z"},"spec":{"finalizers":["kubernetes"]},"status":{"phase":"Active"}}

```