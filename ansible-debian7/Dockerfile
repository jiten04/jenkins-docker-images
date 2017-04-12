FROM debian:7

ENV USER jenkins
ARG DEBIAN_FRONTEND=noninteractive

#install necessary packages
RUN echo 'deb http://http.debian.net/debian wheezy-backports main' > /etc/apt/sources.list.d/backports.list
RUN apt-get update && \
    apt-get -y dist-upgrade
RUN apt-get install -f -y openssh-server git openjdk-7-jre-headless ca-certificates-java && \
    apt-get -t wheezy-backports install -y ansible ca-certificates-java
RUN adduser --disabled-password --gecos "" $USER && \
    echo "$USER:$USER"|chpasswd && \
    adduser $USER sudo
RUN mkdir -p /var/run/sshd

EXPOSE 22