# elasticsearch

```shell
docker run  -d \
-p 9200:9200 \
-p 9300:9300 \
-e ES_JAVA_OPTS="-Xms256m -Xmx256m" \
-e discovery.type=single-node \
--name es \
--restart=always \
elasticsearch:7.12.0
```
