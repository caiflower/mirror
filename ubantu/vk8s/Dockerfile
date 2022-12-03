FROM amd64/ubuntu:22.04

LABEL MAINTAINER=caiflower UBANTUVERSION=22.04 K8SVERSION=v1.22.4 DOCKERVERSION=LASTEST

# 安装docker
RUN apt update && apt install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common  \
    && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - \
    && add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"  \
    && apt update  \
    && apt update  \
    && apt install -y docker-ce docker-ce-cli containerd.io \
    && mkdir /etc/docker \
    && echo << EOF > /etc/docker/daemon.json {"exec-opts": ["native.cgroupdriver=systemd"],"registry-mirrors": ["https://6vu4ghsm.mirror.aliyuncs.com/"]} EOF \

ARG K8SVERSION=v1.22.4-00
ARG KUBEADMINVERSION=1.22.4-00

# 安装kubelet kubectl kubeadm
RUN apt update  \
    && curl https://mirrors.aliyun.com/kubernetes/apt/doc/apt-key.gpg | apt-key add - \
    && echo <<EOF > /etc/apt/sources.list.d/kubernetes.list deb https://mirrors.aliyun.com/kubernetes/apt/ kubernetes-xenial main EOF \
    && apt update \
    && apt-get install -y kubelet=$K8SVERSION kubectl=$K8SVERSION kubeadm=$KUBEADMINVERSION \
