ARG java_vendor=openjdk
ARG java_version=8-alpine

FROM $java_vendor:$java_version

ENV JAVA_OPTS "${JAVA_OPTS} -XX:+UnlockExperimentalVMOptions -XX:+UseCGroupMemoryLimitForHeap"

RUN ["apk", "add",\
  "git",\
  "wget"\
]
#TODO: add other things needed by a Minecraft server

WORKDIR /opt/SpigotMC

ARG BuildTools_version=101
RUN wget https://hub.spigotmc.org/jenkins/job/BuildTools/${BuildTools_version}/artifact/target/BuildTools.jar

ARG SpigotMC_version=latest
#RUN ["java", "-jar", "BuildTools.jar", "--rev", "$SpigotMC_version"]
RUN java -jar BuildTools.jar --rev "${SpigotMC_version}"
RUN ln -vs "${PWD}/spigot-${SpigotMC_version}.jar" /usr/local/bin/spigot

#TODO: VOLUMEs

CMD ["java", "-server", "-jar", "/usr/local/bin/spigot"]
