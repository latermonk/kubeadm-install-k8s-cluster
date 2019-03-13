# kubeadm-install-k8s-cluster

## Task1 install-kubeadm
https://kubernetes.io/docs/setup/independent/install-kubeadm/  

```
//Install
yum install -y chrony

// 启用
systemctl start chronyd
systemctl enable chronyd

// 设置亚洲时区
timedatectl set-timezone Asia/Shanghai

// 启用NTP同步
timedatectl set-ntp yes
```




## Task2 create-cluster-kubeadm
https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/



###  pull kubeadm init需要的镜像

```
kubeadm config images pull
```
### kubeadm init初始化

```
kubeadm init
```



# 参考
k8s安装和集群初始化
https://blog.csdn.net/Blanchedingding/article/details/80861293



# Issues:

```
this Docker version is not on the list of validated versions: 18.09.3. Latest validated version: 18.06
```

