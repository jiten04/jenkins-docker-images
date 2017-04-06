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

#systemd
ENV container docker
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;
VOLUME [ "/sys/fs/cgroup" ]
CMD ["/usr/sbin/init"]

#start ssh server
EXPOSE 22
CMD    ["/usr/sbin/sshd", "-D"]