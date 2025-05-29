Основные понятия:
- Кластер - это группа серверов (нод), которые работают вместе как единая система
- Pod -  минимальная единица запуска. Обычно содержит один контейнер, но может быть несколько.
- Node - физический или виртуальный сервер, на котором работают Pod'ы
- Cluster - совокупность всех нод, управляемая одним Control Plane.
- Kubelet - программа (агент), установленная на ноде.
- kubectl - команда в терминале (утилита), через которую отправляются команды в кластер.

Объекты:
- Deployment - управляет созданием и обновлением Pod'ов
- Service - объект, обеспечивающий стабильный доступ к Pod'ам по IP/имени.
- Ingress - объект для маршрутизации HTTP/HTTPS-запросов (например, по домену или пути).
- ConfigMap / Secret -  объекты, в которых хранятся настройки и секреты (в виде ключ-значение).
- Volume - объект, описывающий подключаемое хранилище.
- Namespace  - логическая область в кластере для изоляции ресурсов.

Главные объекты:

0. Container
1. Pod
2. Deployment
3. Service
4. Nodes
5. Cluster



| Команда  | Действие |
| --- | --- |
| `minikube version` | --- |
| `minikube start` | --- |
| `minikube start --cpus=4 --memory=8gb --disk-size=25gb` | --- |
| `minikube start --driver=docker` | --- |
| `minikube stop` | --- |
| `minikube delete`  | --- |
| `minikube ssh` | подключиться |


| Команда  | Действие |
| --- | --- |
| `kubectl version` | Версия клиента и сервера |
| `kubectl version --client` | Версия клиента |
| `kubectl get componentstatuses` | Показать состояние k8s cluster`a |
| `kubectl cluster-info` | Показать информацию о k8s cluster`a |
| `kubectl get nodes` | Показать все сервера k8s cluster`a  |
| `kubectl apply -f файл.yaml` | применить |


```
kubectl version --client

kubectl apply -f /opt/gvmap/redis-deployment.yaml

sudo systemctl status kubelet

which kubelet
which kubeadm
which kubectl

kubelet --version
kubeadm version
kubectl version --client

kubectl get nodes
kubectl get po -A
kubectl get po -A -o wide
```


```
# https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/

# install packages
sudo apt-get update -y
sudo apt-get install -y apt-transport-https ca-certificates curl

sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt-get update -y
sudo apt-get install -y kubelet kubeadm kubectl containerd
sudo apt-mark hold kubelet kubeadm kubectl


# activate specific modules
# overlay — The overlay module provides overlay filesystem support, which Kubernetes uses for its pod network abstraction
# br_netfilter — This module enables bridge netfilter support in the Linux kernel, which is required for Kubernetes networking and policy.
sudo -i
modprobe br_netfilter
modprobe overlay


# enable packet forwarding, enable packets crossing a bridge are sent to iptables for processing
echo "net.ipv4.ip_forward=1" >> /etc/sysctl.conf
echo "net.bridge.bridge-nf-call-iptables=1" >> /etc/sysctl.conf
sysctl -p /etc/sysctl.conf


# return to user
# In v1.22 and later, if the user does not set the cgroupDriver field under KubeletConfiguration, kubeadm defaults it to systemd.
# by default containerd set SystemdCgroup = false, so you need to activate SystemdCgroup = true, put it in /etc/containerd/config.toml
# https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/configure-cgroup-driver/
# https://kubernetes.io/docs/setup/production-environment/container-runtimes/#cgroup-drivers
sudo mkdir /etc/containerd/
sudo vim /etc/containerd/config.toml

version = 2
[plugins]
  [plugins."io.containerd.grpc.v1.cri"]
   [plugins."io.containerd.grpc.v1.cri".containerd]
      [plugins."io.containerd.grpc.v1.cri".containerd.runtimes]
        [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.runc]
          runtime_type = "io.containerd.runc.v2"
          [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.runc.options]
            SystemdCgroup = true

sudo systemctl restart containerd            


# get master ip for --apiserver-advertise-address
ip a


# to access kubernetes from external network you need to additionaly set flag with external ip --apiserver-cert-extra-sans=158.160.111.211
sudo kubeadm init \
  --apiserver-advertise-address=45.89.24.174 \
  --pod-network-cidr 10.244.0.0/16


# set default kubeconfig
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config


# install cni flannel
kubectl apply -f https://github.com/flannel-io/flannel/releases/latest/download/kube-flannel.yml


# add worker nodes
# kubeadm token generate
# kubeadm token create <generated-token> --print-join-command --ttl=0
sudo kubeadm join 10.128.0.28:6443 --token 7y.z61zq4rzaq3rtipk \
        --discovery-token-ca-cert-hash sha256:e50a7a5b6261746684d033a7d6483ea5b84db8932cb70563b35f91080f7
```


