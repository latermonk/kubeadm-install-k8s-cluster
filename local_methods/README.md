# kubeadm-install-k8s-cluster


#  Local-method


## Task0 preparation

### Install docker

```
cd /etc/yum.repos.d
wget  https://download.docker.com/linux/centos/docker-ce.repo
yum install -y docker-ce

or

yum list docker-ce --showduplicates | sort -r

yum install -y docker-ce-your-specific-version 


or
  
wget https://download.docker.com/linux/centos/7/x86_64/stable/Packages/docker-ce-18.09.3-3.el7.x86_64.rpm

wget https://download.docker.com/linux/centos/7/x86_64/stable/Packages/containerd.io-1.2.4-3.1.el7.x86_64.rpm

wget https://download.docker.com/linux/centos/7/x86_64/stable/Packages/docker-ce-cli-18.09.3-3.el7.x86_64.rpm

then 

yum localinstall  xxx




```

```
systemctl enable docker && systemctl restart docker 
```



## Task1 Installing kubeadm, kubelet and kubectl
https://kubernetes.io/docs/setup/independent/install-kubeadm/  


```
#  001 add rpm source

cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=0
repo_gpgcheck=0
gpgkey=https://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg https://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg
EOF


```

```bash
# 002 Set SELinux in permissive mode (effectively disabling it)

setenforce 0
sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config

swapoff -a

```

```bash
# 003 install 

yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes

systemctl enable --now kubelet

```


## Task2 create-cluster-kubeadm
https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/




### kubeadm init初始化

```
kubeadm init \
--apiserver-advertise-address=192.168.0.182 \
--image-repository registry.aliyuncs.com/google_containers \
--kubernetes-version v1.13.3 \
--service-cidr=10.1.0.0/16\
--pod-network-cidr=10.244.0.0/16


```
### 配置kubectl
```bash
# config kubectl 

mkdir -p $HOME/.kube
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
chown $(id -u):$(id -g) $HOME/.kube/config


```
### 安装flannel 插件
```shell
# install flannel 
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/a70459be0084506e4ec919aa1c114638878db11b/Documentation/kube-flannel.yml
```
### 其它节点加入
```bash
# 
kubeadm join xxx
```



