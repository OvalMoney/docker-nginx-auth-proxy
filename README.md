# Docker image of Nginx Proxy with Basic Auth

[[![Docker Automated build](https://img.shields.io/docker/automated/ovalmoney/docker-nginx-auth-proxy.svg)](https://hub.docker.com/r/ovalmoney/docker-nginx-auth-proxy/)
[![Docker Pulls](https://img.shields.io/docker/pulls/ovalmoney/docker-nginx-auth-proxy.svg)](https://hub.docker.com/r/ovalmoney/docker-nginx-auth-proxy/)
[![Docker Build Status](https://img.shields.io/docker/build/ovalmoney/docker-nginx-auth-proxy.svg)](https://hub.docker.com/r/ovalmoney/docker-nginx-auth-proxy/)

Simple HTTP Proxy with Basic Authentication

```
       w/ user:pass   +------------------------+      +-------------+
User ---------------> | nginx-basic-auth-proxy | ---> | HTTP Server |
                      +------------------------+      +-------------+
```

## Run

```bash
$ docker run \
    --rm \
    --name nginx-basic-auth-proxy \
    -p 8080:80 \
    -p 8090:8090 \
    -e BASIC_AUTH_USERNAME=username \
    -e BASIC_AUTH_PASSWORD=password \
    -e PROXY_PASS=https://www.google.com \
    -e SERVER_NAME=proxy.dtan4.net \
    -e PORT=80 \
    ovalmoney/docker-nginx-auth-proxy
```

Access to http://localhost:8080 , then browser asks you username and password.

You can also try complete HTTP-proxy example using Docker Compose.
hello-world web application cannot be accessed without authentication.

```bash
$ docker-compose up
# http://localhost:8080/
# - Username: username
# - Password: password
```

## Environment variables

### Required

|Key|Description|
|---|---|
|`BASIC_AUTH_USERNAME`|Basic auth username|
|`BASIC_AUTH_PASSWORD`|Basic auth password|
|`PROXY_PASS`|Proxy destination URL|

### Optional

|Key|Description|Default|
|---|---|---|
|`SERVER_NAME`|Value for `server_name` directive|`example.com`|
|`PORT`|Value for `listen` directive|`80`|
|`CLIENT_MAX_BODY_SIZE`|Value for `client_max_body_size` directive|`1m`|
|`PROXY_READ_TIMEOUT`|Value for `proxy_read_timeout` directive|`60s`|
|`WORKER_PROCESSES`|Value for `worker_processes` directive|`auto`|

## License

[![MIT License](http://img.shields.io/badge/license-MIT-blue.svg?style=flat)](LICENSE)
