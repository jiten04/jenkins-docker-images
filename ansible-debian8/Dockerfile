FROM debian:8

ENV USER jenkins
ARG DEBIAN_FRONTEND=noninteractive

#install necessary packages
RUN echo 'deb http://http.debian.net/debian jessie-backports main' > /etc/apt/sources.list.d/backports.list
RUN apt-get update && \
    apt-get -y dist-upgrade
RUN apt-get -t jessie-backports install -y ansible ca-certificates-java && \
    apt-get install -f -y openssh-server git openjdk-8-jre-headless ca-certificates-java
RUN adduser --disabled-password --gecos "" $USER && \
    echo "$USER:$USER"|chpasswd && \
    adduser $USER sudo
RUN mkdir -p /var/run/sshd

EXPOSE 22