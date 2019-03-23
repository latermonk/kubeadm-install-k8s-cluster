# kubeadm-install-k8s-cluster




## Task0 preparation

### Install docker

```
cd /etc/yum.repos.d
wget  https://download.docker.com/linux/centos/docker-ce.repo
yum install -y docker-ce

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
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
exclude=kube*
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



###  pull kubeadm init需要的镜像

```
kubeadm config images pull
```
### kubeadm init初始化

```
kubeadm init --pod-network-cidr=10.244.0.0/16
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


# 参考
k8s安装和集群初始化
https://blog.csdn.net/Blanchedingding/article/details/80861293
