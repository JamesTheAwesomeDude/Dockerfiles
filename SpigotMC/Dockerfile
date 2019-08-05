ARG java_vendor=openjdk
ARG java_version=8-alpine

FROM $java_vendor:$java_version

RUN ["apk", "add",\
  "git",\
  "wget"\
]
#TODO: add other things needed by a Minecraft server

ARG user=mc
ARG BuildTools_version=lastSuccessfulBuild
ARG SpigotMC_version=latest
ENV _JAVA_OPTIONS="${_JAVA_OPTIONS} -XX:+UnlockExperimentalVMOptions -XX:+UseCGroupMemoryLimitForHeap"

WORKDIR /opt/SpigotMC

RUN wget "https://hub.spigotmc.org/jenkins/job/BuildTools/${BuildTools_version}/artifact/target/BuildTools.jar"

RUN HOME="${PWD}" java -jar BuildTools.jar --rev "${SpigotMC_version}" --skip-compile --dev
#prev line to improve caching
RUN HOME="${PWD}" java -jar BuildTools.jar --rev "${SpigotMC_version}" --dev

RUN ln -vs "${PWD}/spigot-${SpigotMC_version}.jar" /usr/local/bin/spigot

VOLUME /var/mc
WORKDIR /var/mc
USER "${user}" #TODO: fix the build failure resulting from running this earlier
ENV HOME="${PWD}"
CMD ["java", "-server", "-jar", "/usr/local/bin/spigot"]
