## units

* REF: <http://www.csdn.net/article/2015-02-27/2824034>



### mongodb example

```
[Unit] 
Description=mongo_rs_1 
After=docker.service 
Requires=docker.service 
[Service] 
TimeoutStartSec=0 
ExecStartPre=-/usr/bin/docker rm mongo_rs_1 
ExecStart=/usr/bin/docker run --name mongo_rs_1 -p 1301:27017 -v /hdd1/mongo_rs_1:/data/db mongo --storageEngine wiredTiger --replSet rs_1
ExecStop=/usr/bin/docker kill mongo_rs_1
[Install] 
WantedBy=multi-user.target

```