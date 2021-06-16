#tomcat-web

```shell
// jdk 8 
FROM dordoka/tomcat
MAINTAINER husiyi
COPY xxx.war /opt/tomcat/webapps/
RUN chmod  777 /opt/tomcat/webapps
ENV JAVA_OPTS "-server -Xms256m -Xmx768m -XX:MaxNewSize=256m -XX:PermSize=128m -XX:MaxPermSize=256m"
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN echo 'Asia/Shanghai' >/etc/timezone
EXPOSE 8080
```
