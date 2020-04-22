FROM alpine:3.11

#Atualizacao do alpine
RUN apk -U upgrade && \
    apk add --no-cache --update bash curl wget \
        tar tzdata iputils unzip findutils git gettext gdb lsof patch \
        libcurl libxml2 libxslt openssl-dev zlib-dev \
        make automake gcc g++ binutils-gold linux-headers paxctl libgcc libstdc++ \
        python gnupg ncurses-libs ca-certificates && \
    update-ca-certificates --fresh && \
    rm -rf /var/cache/apk/*

# Configure JAVA_HOME
RUN apk --update add openjdk7-jre
ENV JAVA_HOME /usr/bin/java

RUN wget -q -O - "https://archive.apache.org/dist/tomcat/tomcat-6/v6.0.53/bin/apache-tomcat-6.0.53.tar.gz" | tar -xzf - -C /opt/

#Estrutura de diretorios para utilizacao da aplicacao
ENV HOME=/opt/app-root
ENV CATALINA_HOME=/opt/apache-tomcat-6.0.53
ENV LOG=/opt/log-app
RUN	mkdir -p ${HOME} && \
    adduser -s /bin/sh -u 1001 -G root -h ${HOME} -S -D default && \
    chown -R 1001:0 ${HOME} && \
    chown -R 1001:0 ${CATALINA_HOME} && \
    chmod -R 775 ${CATALINA_HOME}	&& \
	mkdir -p ${LOG} && \
	chown -R 1001:0 ${LOG} && \
	chmod -R 775 ${LOG}	

WORKDIR ${CATALINA_HOME}
EXPOSE 8080
CMD [ "java", "-jar", "bin/bootstrap.jar" ]
