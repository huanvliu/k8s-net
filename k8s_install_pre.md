### 物理环境
1. 一台或多台下列机器之一
- Ubuntu 16.04+
- Debian 9
- CentOS 7
- RHEL 7
- Fedora 25/26 (best-effort)
- HypriotOS v1.0.1+
- Container Linux (tested with 1800.6.0)
2. 机器配置
* 每台机器至少2G内存
* 2核cpu
* 网络liantong
* 使用的端口开放
* host唯一
* 必须禁止swap

### 运行时软件环境
+ docker
+ cri-o
+ frakti
+ rkt
---
### 安装kubeadm，kubelet，kubectl
 1.不同环境下的安装，但必须解决科学上网问题
  * **Ubuntu, Debian or HypriotOS sh :**
    `apt-get update && apt-get install -y apt-transport-https curl
    curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
    cat <<EOF >/etc/apt/sources.list.d/kubernetes.list
    deb https://apt.kubernetes.io/ kubernetes-xenial main
    EOF
    apt-get update
    apt-get install -y kubelet kubeadm kubectl
    apt-mark hold kubelet kubeadm kubectl`
  * **CentOS, RHEL or Fedora sh :**
    `cat <<EOF > /etc/yum.repos.d/kubernetes.repo
    [kubernetes]
    name=Kubernetes
    baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
    enabled=1
    gpgcheck=1
    repo_gpgcheck=1
    gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
    exclude=kube*
    EOF
    \# Set SELinux in permissive mode (effectively disabling it)
    setenforce 0
    sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config

    yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes

    systemctl enable kubelet && systemctl start kubelet`
  * **Container Linux sh :**
     `RELEASE="\$(curl -sSL https://dl.k8s.io/release/stable.txt)"
    mkdir -p /opt/bin
    cd /opt/bin

    curl -L --remote-name-all https://storage.googleapis.com/kubernetes-release/release/${RELEASE}/bin/linux/amd64/{kubeadm,kubelet,kubectl}
    chmod +x {kubeadm,kubelet,kubectl}

    curl -sSL "https://raw.githubusercontent.com/kubernetes/kubernetes/\${RELEASE}/build/debs/kubelet.service" | sed "s:/usr/bin:/opt/bin:g" > /etc/systemd/system/kubelet.service
    mkdir -p /etc/systemd/system/kubelet.service.d
    curl -sSL "https://raw.githubusercontent.com/kubernetes/kubernetes/\${RELEASE}/build/debs/10-kubeadm.conf" | sed "s:/usr/bin:/opt/bin:g" > /etc/systemd/system/kubelet.service.d/10-kubeadm.conf`

2. 启动kebelet
   systemctl enable kubelet && systemctl start kubelet
---
详情参考[官方文档](https://kubernetes.io/docs/setup/independent/install-kubeadm/#installing-runtime)


