# docker-training

## Prerequisite:
- Docker hub account: https://hub.docker.com/signup?next=%2F%3Foverlay%3Donboarding
- Docker: https://hub.docker.com/?overlay=onboarding
- Gitbash:  https://gitforwindows.org/


# Scenario 1
- baseimage: java
- install script to remove a file
- install wso2esb

## Prerequisite
- download wso2esb in local
from [here](https://wso2.com/integration/previous-releases/?utm_source=esb_page&utm_medium=esb_page&utm_campaign=esb_page)


## docker image build
- Dockerfile
- Provide instructions

file: Dockerfile
```docker
FROM openjdk:8-jre-alpine

ARG WSO2_SERVER_VERSION=${WSO2_SERVER_VERSION:-4.9.0}
ARG PRODUCT_ID=${PRODUCT_ID:-enterprise-service-bus}
ARG WSO2_SERVER=${WSO2_SERVER:-wso2esb}
ARG PRODUCT_USER=${PRODUCT_USER:-wso2user}
ARG PRODUCT_REPOSITORY=${PRODUCT_REPOSITORY:-'https://product-dist.wso2.com/products'}

RUN addgroup -S ${PRODUCT_USER} && adduser -S -g ${PRODUCT_USER} ${PRODUCT_USER}

RUN apk add --no-cache --update-cache \
	  ca-certificates \
	  unzip \
      wget \
	  && \
    wget \
	  --progress=dot:giga \
	  --referer="http://connect.wso2.com/wso2/getform/reg/new_product_download" \
	  -O "/tmp/${WSO2_SERVER}-${WSO2_SERVER_VERSION}.zip" \
	  "${PRODUCT_REPOSITORY}/${PRODUCT_ID}/${WSO2_SERVER_VERSION}/${WSO2_SERVER}-${WSO2_SERVER_VERSION}.zip" && \
    unzip /tmp/${WSO2_SERVER}-${WSO2_SERVER_VERSION}.zip -d /opt && \
	chmod o-rwx -R /opt/${WSO2_SERVER}-${WSO2_SERVER_VERSION} && \
	chown ${PRODUCT_USER}:${PRODUCT_USER} -R /opt/${WSO2_SERVER}-${WSO2_SERVER_VERSION} && \
    rm /tmp/${WSO2_SERVER}-${WSO2_SERVER_VERSION}.zip && \
    apk del \
	  ca-certificates \
	  unzip \
      wget 

USER ${PRODUCT_USER}

EXPOSE 9443 9763 8243 8280
WORKDIR /opt/${WSO2_SERVER}-${WSO2_SERVER_VERSION}
ENTRYPOINT ["bin/wso2server.sh"]

```


- Build

```sh
docker build . -t dhaks/wso2esb:1.0.0
```
validate image
```
docker images
```

## docker run

```
docker run dhaks/wso2esb:1.0.0
```
## other commands
```bash
docker pull ubuntu
docker images
docker pull alpine
docker images
docker container
docker container ls
docker build . -t dhaks/wso2esb:1.0.0
docker run dhaks/wso2esb:1.0.0
```

