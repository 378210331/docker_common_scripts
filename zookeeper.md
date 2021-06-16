# zookeeper

```shell
mkdir -p  ~/docker/zookeeper

docker run -d \
-p 2181:2181 \
-v ~/docker/zookeeper/data:/data \
-v ~/docker/zookeeper/conf:/conf \
-v ~/docker/zookeeper/datalog:/datalog \
-v ~/docker/zookeeper/log:/log \
--name=zk \
--restart=always \
zookeeper:3.7.0
```
