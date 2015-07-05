etcd
========

### etcd RESTful API

```
  
curl http://127.0.0.1:4001/v2/stats/self
curl -L http://127.0.0.1:4001/v2/stats/leader
curl http://127.0.0.1:4001/v2/stats/store
curl http://127.0.0.1:7001/v2/admin/config

```


## get service related files

```
systemctl cat etcd

``` 

## etcd data location: 

```
 /var/lib/etcd/*
```


ssh srv3-9 "/etc/init.d/nodejs-wifi-storage restart"
ssh srv3-10 "/etc/init.d/nodejs-wifi-storage restart"
ssh srv3-11 "/etc/init.d/nodejs-wifi-storage restart"
ssh srv3-12 "/etc/init.d/nodejs-wifi-storage restart"




apt-get purge mongodb-org mongodb-org-server mongodb-org-mongos mongodb-org-shell mongodb-org-tools -y


apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
apt-get install -y lsb-release 
echo "deb http://repo.mongodb.org/apt/debian "$(lsb_release -sc)"/mongodb-org/3.0 main" |  tee /etc/apt/sources.list.d/mongodb-org-3.0.list
apt-get update 
apt-get install -y mongodb-org



"_id" : "wifi_stats",  "host" : "wifi_stats/10.11.1.7:1304,10.11.1.8:1304,mongo-xiaoyun-1-1:1201" }
	{  "_id" : "wifi_stats2",  "host" : "wifi_stats2/10.11.1.13:1302,10.11.1.14:1302,mongo-xiaoyun-1-2:1202" }
	{  "_id" : "xiaoyun_3",  "host" : "xiaoyun_3/10.11.1.21:1302,10.11.1.22:1302,mongo-xiaoyun-1-3:1203" }
	{  "_id" : "xiaoyun_4",  "host" : "xiaoyun_4/10.11.1.24:1302,10.11.1.25:1302,mongo-xiaoyun-1-4:1204" }
	{  "_id" : "xiaoyun_5",  "host" : "xiaoyun_5/10.11.1.27:1302,10.11.1.28:1302,mongo-xiaoyun-1-5:1205" }
	
	