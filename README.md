# docker-apache2-php82-fpm
minimal alpine based image with apache2 and php-fpm82

.env file get bypassed by manually set environment variables from portainer gui

Docker hub: https://hub.docker.com/r/braingremlin/apache2-php82-fpm

## Build ##

sudo docker buildx build --platform linux/amd64,linux/arm64 -t braingremlin/apache2-php82-fpm:latest -t braingremlin/apache2-php82-fpm:V --push .


## XDEBUG ##

PHP Xdebug (https://xdebug.org/) is installed but not enabled by default

Use environment variable

`XDEBUG=true`

to enable

## Networking ##
If you are using a reverse proxy on the same container environment you should set a common network for the proxy and all the proxied services, so you can access those services directly by docker internal network using the container name, i.e.:

`http://mycontainer:80`

**to connect use the EXPOSED port not the PUBLISHED!**



```yaml
services:
  mycontainer:
    container_name: mycontainer
    .
    .
    .
    networks:
      - npm-bridge
    ports:
      - ${EXTERNAL_PORT:-8888}:80 # use 80 instead of EXTERNAL_PORT to access this service from internal docker network

networks:
  npm-bridge:
    name: npm_bridge
```
