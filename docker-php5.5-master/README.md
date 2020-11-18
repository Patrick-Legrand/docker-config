# Docker with Apache/PHP5.5/XDebug

Simple docker configuration with apache/php5.5/xdebug

## Configuration

In the docker directory, change the vhost and the **php.ini** configuration if needed

## Launch

```sh
docker-compose build
docker-compose start
docker container ls

# Replace CONTAINER_ID with the php55 container id
docker exec -it -u root CONTAINER_ID bash
```
