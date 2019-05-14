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


