FROM openjdk:14-jdk-oracle
RUN groupadd -g 1000 devmind && \
    useradd -r -u 1000 -g devmind devmind
USER devmind

RUN mkdir -p /usr/local/application
ADD ["./application.zip", "/usr/local/application/"]
RUN chown -R devmind:devmind /usr/local/application

#USER devmind
# TODO entrypoint and command
