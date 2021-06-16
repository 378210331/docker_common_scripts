# nginx 

### 目标挂载路径
- /etc/nginx  -> /nginx/conf
- /usr/share/nginx/html -> /nginx/html
-  /var/log/nginx/ -> /nginx/log
- /usr/share/nginx/others -> /nginx/others


- 1运行nginx ,准备配置文件
```shell
docker run -d --name nginx nginx
```
- 2提取文件至将要挂载的目录
```shell
mkdir /nginx
docker cp nginx:/etc/nginx /nginx/conf ;
docker cp nginx:/usr/share/nginx/html  /nginx/html ;
docker cp nginx:/var/log/nginx  /nginx/log ;
```
- 3删除原nginx
```shell
docker rm -f nginx
```

- 4建立挂载的nginx
```shell
docker run -d -p 80:80 \
--name=nginx --restart=always \
-v /nginx/conf:/etc/nginx \
-v /nginx/html:/usr/share/nginx/html \
-v /nginx/others:/usr/share/nginx/others \
-v /nginx/log:/var/log/nginx \
nginx
```

- 5修改nginx.conf以root用户运行

## 纯镜像打包处理
针对云环境等避免采用文件挂载的系统，可以将dist文件打包至镜像中,以镜像为模板
- 1.准备Dockerfile文件,参考如下
```dockerfile
FROM nginx
MAINTAINER husiyi
COPY dist /usr/share/nginx/html
RUN chmod +x 777 /usr/share/nginx/html
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN echo 'Asia/Shanghai' >/etc/timezone
EXPOSE 80
```

- 2.将dist文件夹与Dockerfile 置于一个文件夹,运行命令生成镜像
```dockerfile
    docker build -t front:1.0 ./
```
