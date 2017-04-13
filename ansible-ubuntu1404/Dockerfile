FROM ubuntu:14.04

ENV USER jenkins
ARG DEBIAN_FRONTEND=noninteractive

#install necessary packages
RUN apt-get update && \
    apt-get -y dist-upgrade
RUN apt-get install -y software-properties-common && \
    add-apt-repository ppa:ansible/ansible && \
    apt-get update
RUN apt-get install -y openssh-server git ansible openjdk-7-jre
RUN adduser --disabled-password --gecos "" $USER && \
    echo "$USER:$USER"|chpasswd && \
    adduser $USER sudo
RUN mkdir -p /var/run/sshd

EXPOSE 22