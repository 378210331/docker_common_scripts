# mariadb

```shell
docker run -d \
-p 3306:3306 \
-v ~/docker/mysql/data:/var/lib/mysql \
-v ~/docker/mysql/log:/var/log/mysql \
-v /etc/localtime:/etc/localtime:ro \
-e MARIADB_ROOT_PASSWORD=root \
--name mysql \
--restart=always \
mariadb:10.3.32 --lower_case_table_names=1
```

## 修改最大连接数和大小写不敏感
```shell
docker exec -it mysql /bin/bash -c "echo lower_case_table_names=1 >> /etc/mysql/mariadb.cnf";
docker exec -it mysql /bin/bash -c "echo max_allowed_packet=64M >> /etc/mysql/mariadb.cnf";
docker exec -it mysql /bin/bash -c "echo max_connections=1500 >> /etc/mysql/mariadb.cnf";
docker restart mysql;
```
