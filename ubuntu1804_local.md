# aliyun

```
apt-get update && apt-get install -y apt-transport-https
curl https://mirrors.aliyun.com/kubernetes/apt/doc/apt-key.gpg | apt-key add - 
cat <<EOF >/etc/apt/sources.list.d/kubernetes.list
deb https://mirrors.aliyun.com/kubernetes/apt/ kubernetes-xenial main
EOF  
apt-get update
apt-get install -y kubelet kubeadm kubectl
```


# ubuntu snapInstall


1.前往 [https://uappexplorer.com/snaps](https://uappexplorer.com/snaps) 搜索需要的 snap 包， 例如 `RedisDesktopManager`

2.载对应架构的 snap 包

3.install

```
sudo snap install xxx.snap --dangerous --classic
```

# 查看相关的安装包


```
kubeadm config images list
```


```
k8s.gcr.io/kube-apiserver:v1.14.1
k8s.gcr.io/kube-controller-manager:v1.14.1
k8s.gcr.io/kube-scheduler:v1.14.1
k8s.gcr.io/kube-proxy:v1.14.1
k8s.gcr.io/pause:3.1
k8s.gcr.io/etcd:3.3.10
k8s.gcr.io/coredns:1.3.1

```
使用docker pull依次拉去镜像

