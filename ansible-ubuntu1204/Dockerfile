FROM ubuntu:12.04

ENV USER jenkins
ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get -y dist-upgrade
RUN apt-get install -y python-software-properties && add-apt-repository ppa:openjdk-r/ppa && apt-add-repository ppa:ansible/ansible && apt-get update
RUN apt-get install -y openssh-server openjdk-8-jdk git ansible
RUN adduser --disabled-password --gecos "" $USER && echo "$USER:$USER"|chpasswd && adduser $USER sudo
RUN mkdir /var/run/sshd

EXPOSE 22
CMD    ["/usr/sbin/sshd", "-D"]
