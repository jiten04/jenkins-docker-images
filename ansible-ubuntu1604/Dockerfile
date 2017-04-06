FROM ubuntu:16.04

ENV USER jenkins
ARG DEBIAN_FRONTEND=noninteractive

#systemd trickery
RUN find /etc/systemd/system \
         /lib/systemd/system \
         -path '*.wants/*' \
         -not -name '*journald*' \
         -not -name '*systemd-tmpfiles*' \
         -not -name '*systemd-user-sessions*' \
         -exec rm \{} \;

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

#systemd trickery
VOLUME ["/sys/fs/cgroup"]
VOLUME ["/run"]
CMD ["/sbin/init"]

#start ssh server
EXPOSE 22
CMD    ["/usr/sbin/sshd", "-D"]