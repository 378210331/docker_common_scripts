# mysql 8

```shell
docker run -d \
-p 3306:3306 \
-v ~/docker/mysql/data:/var/lib/mysql \
-v ~/docker/mysql/log:/var/log/mysql \
-v /etc/localtime:/etc/localtime:ro \
-e MYSQL_ROOT_PASSWORD=root \
--name mysql \
--restart=always \
mysql:8.0.23 --lower_case_table_names=1
```

## 修改最大连接数和大小写不敏感
```shell
docker exec -it mysql /bin/bash -c "echo lower_case_table_names=1 >> /etc/mysql/my.cnf";
docker exec -it mysql /bin/bash -c "echo max_connections=1500 >> /etc/mysql/my.cnf";
docker restart mysql;
```
