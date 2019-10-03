FROM openjdk:8-alpine
COPY ./myDelScript.sh /tmp/
COPY ./entrypoint.sh /opt/
RUN ls -ltr /opt
RUN unzip --help
RUN env
# COPY ../../resources/wso2esb-4.9.0.zip /opt
#RUN unzip
WORKDIR /opt
#RUN 
CMD ["/bin", "/opt/entrypoint.sh"]