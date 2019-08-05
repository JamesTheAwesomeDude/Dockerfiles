ARG java_vendor=openjdk
ARG java_version=8-alpine

FROM $java_vendor:$java_version

RUN ["apk", "add",\
  "git",\
  "wget"\
]
#TODO: add other things needed by a Minecraft server

ARG user=mc
WORKDIR /opt/SpigotMC
RUN chown -v "${user}" "${PWD}"

ARG BuildTools_version=lastSuccessfulBuild
RUN wget "https://hub.spigotmc.org/jenkins/job/BuildTools/${BuildTools_version}/artifact/target/BuildTools.jar"

#USER "${user}"
ENV _JAVA_OPTIONS="${_JAVA_OPTIONS} -XX:+UnlockExperimentalVMOptions -XX:+UseCGroupMemoryLimitForHeap"

ARG SpigotMC_version=latest
RUN HOME="${PWD}" java -jar BuildTools.jar --rev "${SpigotMC_version}" --skip-compile --dev
#prev line to improve caching
RUN HOME="${PWD}" java -jar BuildTools.jar --rev "${SpigotMC_version}" --dev

#USER root
RUN ln -vs "${PWD}/spigot-${SpigotMC_version}.jar" /usr/local/bin/spigot
#USER "${user}"

VOLUME /var/mc
WORKDIR /var/mc
CMD ["java", "-server", "-jar", "/usr/local/bin/spigot"]
