#tomcat-web

```shell
FROM tomcat:8.5.70-jre8-openjdk-slim
MAINTAINER husiyi
ARG TARGET
ARG PORT
COPY $TARGET /usr/local/tomcat/webapps/$TARGET
RUN chmod  777 /usr/local/tomcat/webapps
ENV JAVA_OPTS "-server -Xms1024m -Xmx1024m -XX:MaxNewSize=256m -XX:PermSize=512m -XX:MaxPermSize=512m"
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN echo 'Asia/Shanghai' >/etc/timezone
EXPOSE $PORT
```
修改rebuild.sh中的参数,使用sh rebuild.sh 进行迭代版本

```shell
#!/bin/bash
#--------------------------------------------
# 脚本说明
# author：hsy
# 配置下面参数，docker build 和docker run 的参数
# IMAGE_NAME 生成的镜像名称(必填)
# VERSION 生成的镜像版本(必填)
#  PORT 容器监听端口号(必填)
# TARGET 往镜像里面添加的内容名称
# EVNS 环境变量数组,选填，示例在下方
#--------------------------------------------

#镜像名称
IMAGE_NAME=cas
#版本
VERSION=latest
#占用端口
PORT=8080

#添加到镜像的文件,一般是war,war解压文件夹,jar名称
TARGET=cas

#环境变量,示例如下
ENVS=(
)

:<<EOF
下面的ENVS已注释,JAVA_OPTS请在最下方修改
ENVS=(
"-e NACOS_HOST=172.16.11.75:30848"
"-e SPRING_PROFILES_ACTIVE=prod"
)
EOF

PWD=`pwd`

if [ ! $IMAGE_NAME ]; then  
  echo "镜像名称IMAGE_NAME不能为空"  
  exit 1
fi 

if [ ! $VERSION ]; then  
  echo "版本version不能为空"  
  exit 1
fi 

if [ ! $PORT ]; then  
  echo "端口port不能为空"  
  exit 1
fi 

if [ ! $TARGET ]; then  
  echo "添加到镜像的文件target不能为空"  
  exit 1
fi 


echo "开始构造新镜像"
docker build -t $IMAGE_NAME:$VERSION \
--build-arg TARGET=$TARGET \
--build-arg PORT=$PORT ./
echo "新镜像构造完毕,准备替换应用"
docker rm -f $IMAGE_NAME
echo "新镜像构造完毕,准备替换应用"
docker run -itd --name=$IMAGE_NAME \
-p $PORT:8080 \
-v $PWD/logs:/usr/local/tomcat/logs \
${ENVS[@]} \
--restart=always \
$IMAGE_NAME:$VERSION
echo "重启应用完毕，输出日志"
docker logs -f $IMAGE_NAME
```
