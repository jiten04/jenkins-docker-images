FROM centos:7

ENV USER jenkins
RUN yum install -y epel-release
RUN yum update -y && yum install -y openssh-server java-1.8.0-openjdk-devel git ansible
RUN adduser $USER && echo "$USER:$USER"|chpasswd && usermod -aG wheel $USER
RUN mkdir /var/run/sshd

EXPOSE 22
CMD    ["/usr/sbin/sshd", "-D"]