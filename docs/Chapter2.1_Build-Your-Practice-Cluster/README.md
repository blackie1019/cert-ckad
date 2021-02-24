# Chapter2 : Build Your Practice Cluster

https://learn.acloud.guru/course/d068441f-75b4-4fe8-a7a6-df9153f24a35/learn/638c1a6b-7159-4c72-968c-7b13c2232da3/b86ec97f-f2e8-4a8b-b969-4249553ff582/watch

## Create Cloud Servers

CentOS8, Medium Size

- Kube Master

  54.254.246.233
  172.31.20.33

- Kube Worker 1

  13.212.235.32
  172.31.16.60

- Kube Worker 2

  54.179.39.151
  172.31.20.13

## Commands

先使用 `sudo -s` ，則 `sudo` 皆可移除．且 `cat` 等指令不會出錯

### Master and all worknode need to install:

- install docker-ce
- install kubelet, kubeadm, kubectl
- hold command for docker-ce, kubelet, kubetadm, kubectl
- `echo "net.bridge.bridge-nf-call-iptables=1" | sudo tee -a /etc/sysctl.conf`
- `sudo sysctl -p`

---

Reference : [](https://www.tecmint.com/install-a-kubernetes-cluster-on-centos-8/)

### Docker CE

```sh
dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo

dnf install -y https://download.docker.com/linux/centos/7/x86_64/stable/Packages/containerd.io-1.4.3-3.1.el7.x86_64.rpm

dnf install -y docker-ce docker-ce-cli
systemctl enable docker
systemctl start docker
```

### Kubernetes(Kubeadm)

```sh
cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF

dnf install kubeadm -y
systemctl enable kubelet
systemctl start kubelet 
```

``` Turn-off Swap and setenforce 0, reboot
swapoff -a
setenforce 0
sed -i --follow-symlinks 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/sysconfig/selinux
reboot
```

### Firewall

#### Master

```sh
firewall-cmd --permanent --add-port=6443/tcp
firewall-cmd --permanent --add-port=2379-2380/tcp
firewall-cmd --permanent --add-port=10250/tcp
firewall-cmd --permanent --add-port=10251/tcp
firewall-cmd --permanent --add-port=10252/tcp
firewall-cmd --permanent --add-port=10255/tcp
firewall-cmd --reload
modprobe br_netfilter
echo '1' > /proc/sys/net/bridge/bridge-nf-call-iptables
```

#### Work Nodes

```sh
setenforce 0
sed -i --follow-symlinks 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/sysconfig/selinux
firewall-cmd --permanent --add-port=6783/tcp
firewall-cmd --permanent --add-port=10250/tcp
firewall-cmd --permanent --add-port=10255/tcp
firewall-cmd --permanent --add-port=30000-32767/tcp
firewall-cmd --reload
echo '1' > /proc/sys/net/bridge/bridge-nf-call-iptables
```

### Master Init

`sudo kubeadm init --pod-network-cidr=10.244.0.0/16`

---

To start using your cluster, you need to run the following as a regular user:

```sh
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
Alternatively, if you are the root user, you can run:

  export KUBECONFIG=/etc/kubernetes/admin.conf

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

Then you can join any number of worker nodes by running the following on each as root:

```sh
kubeadm join 172.31.20.33:6443 --token ctbbdo.pnvi47m9mokvbu09 --discovery-token-ca-cert-hash sha256:3c34515b3e5aa33bcc6779b107617d60a91ef15f6c18186f42a3623860bef400
```

###  選擇安裝 flannel

```sh
kubectl apply -f https://github.com/coreos/flannel/raw/master/Documentation/kube-flannel.yml
```
### WorkNode Add into Cluster

```sh
kubeadm join 172.31.20.33:6443 --token ctbbdo.pnvi47m9mokvbu09 --discovery-token-ca-cert-hash sha256:3c34515b3e5aa33bcc6779b107617d60a91ef15f6c18186f42a3623860bef400
```

## Reference 

- [How to Install a Kubernetes Cluster on CentOS 8](https://www.tecmint.com/install-a-kubernetes-cluster-on-centos-8/)