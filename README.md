# Docker-training
## Description
You will get to know basic commands and run your first program with WSO2 esb.
## Prerequisite:
- Docker hub account: https://hub.docker.com/signup?next=%2F%3Foverlay%3Donboarding
- Docker: https://hub.docker.com/?overlay=onboarding
- Gitbash:  https://gitforwindows.org/
```bash
docker pull ubuntu
docker images
docker pull alpine
docker images
docker container
docker container ls
```


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
FROM openjdk:8-alpine
COPY ./myDelScript.sh /tmp/
COPY ./entrypoint.sh /opt/
RUN touch testing.txt
RUN ls -ltr /opt
RUN unzip --help
RUN env
# COPY ../../resources/wso2esb-4.9.0.zip /opt
#RUN unzip
WORKDIR /opt
#RUN
CMD ["sh", "/opt/entrypoint.sh"]

```


- Build

```sh
docker build . -t "dhaks/intro:1.0.0"
```
validate image
```
docker images
```

## Run
```
docker run dhaks/intro:1.0.0 -p 9443:9443 -p 9763:9763 -p 8243:8243 -p 8280:8280 -name wso2-esb
```

## Test
```
Go to your browser and paste the following URL (https://localhost:9443/carbon)
```
