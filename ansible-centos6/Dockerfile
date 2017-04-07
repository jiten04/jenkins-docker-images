FROM centos:6

ENV USER jenkins

#install necessary packages
RUN yum install -y epel-release
RUN yum update -y && \
    yum install -y java-1.8.0-openjdk-devel git ansible
RUN adduser $USER && \
    echo "$USER:$USER"|chpasswd && \
    usermod -aG wheel $USER