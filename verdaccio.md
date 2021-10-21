# verdaccio

#镜像拉取,运行
```shell
docker pull verdaccio/verdaccio
```

```shell
docker run -d --name=verdaccio verdaccio/verdaccio
```

#拷贝配置文件和目录
```shell
mkdir ~/docker/verdaccio
```

```shell
docker cp verdaccio:/verdaccio/storage/data ~/docker/verdaccio/data;
docker cp verdaccio:/verdaccio/conf ~/docker/verdaccio/conf;
docker cp verdaccio:/verdaccio/plugins ~/docker/verdaccio/plugins;
```


#更改权限
```shell
sudo chown -R 10001:65533 ~/docker/verdaccio
```

#镜像构建

```shell
docker run -d \
-p 4873:4873 \
-v ~/docker/verdaccio/data:/verdaccio/storage/data \
-v ~/docker/verdaccio/conf:/verdaccio/conf \
-v ~/docker/verdaccio/plugins:/verdaccio/plugins \
--name=verdaccio \
--restart=always \
verdaccio/verdaccio
```
 
 
 
 
