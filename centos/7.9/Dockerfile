FROM centos:7.9.2009

MAINTAINER by lijinlong100

RUN mv /etc/yum.repos.d /etc/yum.repos.d.bak \
    && mkdir /etc/yum.repos.d \
    && curl -o /etc/yum.repos.d/CentOS-7.repo http://mirrors.aliyun.com/repo/Centos-7.repo \
    && yum makecache \
    && yum -y install openssh-clients.x86_64 openssh-server vim python3 \
    && mkdir /var/run/sshd \
    && echo "HostKey /root/.ssh/id_rsa" >> /etc/ssh/sshd_config

RUN rm -rf /usr/bin/systemctl \
    && curl -o /usr/bin/systemctl https://raw.githubusercontent.com/gdraheim/docker-systemctl-replacement/master/files/docker/systemctl3.py \
    && chmod a+x /usr/bin/systemctl \
    && ssh-keygen -t rsa -b 2048 -f /etc/ssh/ssh_host_rsa_key \
    && systemctl start sshd \
    && systemctl enable sshd

# COPY ./CentOS-7.repo /etc/yum.repos.d/CentOS-7.repo
# COPY ./epel.repo /etc/yum.repos.d/epel.repo
# COPY ./epel.repo.rpmnew /etc/yum.repos.d/epel.repo.rpmnew

EXPOSE 22