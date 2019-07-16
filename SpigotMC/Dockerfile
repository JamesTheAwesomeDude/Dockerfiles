FROM alpine:latest
RUN apk --update add openjdk8-jre
#TODO: replace above with actual jre image

RUN apk add\
 git\
 wget

#TODO: add other things needed by a Minecraft server

WORKDIR /opt/SpigotMC

ARG BuildTools_version=101
RUN wget https://hub.spigotmc.org/jenkins/job/BuildTools/${BuildTools_version}/artifact/target/BuildTools.jar
# https://docs.docker.com/v17.09/engine/userguide/eng-image/dockerfile_best-practices/#add-or-copy

ARG SpigotMC_version=1.14.3
RUN java -jar BuildTools.jar --rev ${SpigotMC_version}
RUN ln -vs "${PWD}/spigot-${SpigotMC_version}.jar" /usr/local/bin/spigot

#TODO: VOLUMEs

ENTRYPOINT java -server -jar /usr/local/bin/spigot
