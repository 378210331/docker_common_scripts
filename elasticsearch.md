# elasticsearch

```shell
mkdir -p ~/docker/es/{data,plugins}
chmod 777 -R ~/docker/es
```

```shell
docker run  -d \
-e ES_JAVA_OPTS="-Xms512m -Xmx512m" \
-e discovery.type=single-node \
-v ~/docker/es/data:/usr/share/elasticsearch/data \
-v ~/docker/es/plugins:/usr/share/elasticsearch/plugins \
--name es \
--restart=always \
elasticsearch:7.12.0
```
