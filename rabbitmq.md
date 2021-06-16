# rabbitmq

```shell
docker run -dit \
-p 5672:5672 \
-p 15672:15672 \
-e RABBITMQ_DEFAULT_USER=admin \
-e RABBITMQ_DEFAULT_PASS=admin \
--name=rabbitmq \
rabbitmq:management
```
