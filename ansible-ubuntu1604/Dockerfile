FROM ubuntu:16.04

ENV USER jenkins
ARG DEBIAN_FRONTEND=noninteractive

#install necessary packages
RUN apt-get update &&\
    apt-get -y dist-upgrade
RUN apt-get install -y software-properties-common && \
    apt-add-repository ppa:ansible/ansible && \
    apt-get update
RUN apt-get install -y openssh-server openjdk-8-jdk git ansible
RUN adduser --disabled-password --gecos "" $USER && \
    echo "$USER:$USER"|chpasswd && \
    adduser $USER sudo
RUN mkdir /var/run/sshd

#copy systemctl replacement
#https://github.com/gdraheim/docker-systemctl-replacement
RUN test -d /run/systemd/system || mkdir /run/systemd/system
RUN apt-get install systemd && apt-mark hold systemd
COPY docker-systemctl-replacement/files/docker/systemctl.py /usr/bin/systemctl

#start ssh server
EXPOSE 22
CMD    ["/usr/sbin/sshd", "-D"]