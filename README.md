# dev_Kubernetes
Kubernetes Development/Deployment

#### Configure Kubernetes Repository
```
$cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF
```

#### Install kubelet, kubeadm, and kubectl (RHEL7)
```
$sudo yum install -y kubelet kubeadm kubectl
$sudo systemctl enable kubelet
$sudo systemctl start kubelet
```

#### Install for Mac
- Installing Docker
  - [https://docs.docker.com/install/ #supported-platforms](https://docs.docker.com/install/ #supported-platforms) <br/>

- Installing kubectl
  - [https://kubernetes.io/docs/tasks/tools/install-kubectl/](https://kubernetes.io/docs/tasks/tools/install-kubectl/) <br/>

- Installing Minikube
  - [https://kubernetes.io/docs/tasks/tools/install-minikube/](https://kubernetes.io/docs/tasks/tools/install-minikube/) <br/>

#### Set Hostnames on Nodes
```
$sudo hostnamectl set-hostname master-node
$sudo hostnamectl set-hostname worker-node1

$sudo vi /etc/hosts

192.168.1.10 master.local master-node
192.168.1.20 node1.local node1 worker-node
```

#### Configure Firewall
# On Master-node: <br/>
```
$sudo firewall-cmd --permanent --add-port=6443/tcp
$sudo firewall-cmd --permanent --add-port=2379-2380/tcp
$sudo firewall-cmd --permanent --add-port=10250/tcp
$sudo firewall-cmd --permanent --add-port=10251/tcp
$sudo firewall-cmd --permanent --add-port=10252/tcp
$sudo firewall-cmd --permanent --add-port=10255/tcp
$sudo firewall-cmd --reload
```

# On worker-node: <br/>
```
$sudo firewall-cmd --permanent --add-port=10251/tcp
$sudo firewall-cmd --permanent --add-port=10255/tcp
$firewall-cmd --reload
```

#### Update IPTables Settings
```
cat <<EOF > /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
sysctl --system
```

#### Disable SELinux
```
$sudo setenforce 0
$sudo sed -i ‘s/^SELINUX=enforcing$/SELINUX=permissive/’ /etc/selinux/config
```

#### Disable SWAP
```
$sudo sed -i '/swap/d' /etc/fstab
$sudo swapoff -a

```
