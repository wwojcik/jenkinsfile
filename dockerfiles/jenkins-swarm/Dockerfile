FROM docker
ENV LANG C.UTF-8
RUN { \
		echo '#!/bin/sh'; \
		echo 'set -e'; \
		echo; \
		echo 'dirname "$(dirname "$(readlink -f "$(which javac || which java)")")"'; \
	} > /usr/local/bin/docker-java-home \
	&& chmod +x /usr/local/bin/docker-java-home
ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk
ENV PATH $PATH:$JAVA_HOME/bin

ENV JAVA_VERSION 8u92
ENV JAVA_ALPINE_VERSION 8.92.14-r0

RUN set -x \
	&& apk add --no-cache \
		git py-pip openjdk8="$JAVA_ALPINE_VERSION" \
	&& [ "$JAVA_HOME" = "$(docker-java-home)" ]

RUN mkdir -p /opt/swarm-client \
    && wget http://repo.jenkins-ci.org/releases/org/jenkins-ci/plugins/swarm-client/2.0/swarm-client-2.0-jar-with-dependencies.jar -O /opt/swarm-client/swarm-client.jar \
    && pip install docker-compose \
    && addgroup docker \
    && adduser -D jenkins -G docker \
    && rm -rf /var/cache/apk/*

CMD java -jar /opt/swarm-client/swarm-client.jar -master $JENKINS_URL -username $JENKINS_USER -password $JENKINS_PASSWORD -executors 1  -fsroot /home/jenkins/
