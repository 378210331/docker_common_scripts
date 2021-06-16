# nexus2

````shell
docker run -d \
-p 8081:8081 \
--name  nexus \
--restart=always \
-v  /nexus/nexus-data:/nexus-data  \
-v  /nexus/sonatype-work:/sonatype-work  \
-u root \
sonatype/nexus:2.14.8
````
