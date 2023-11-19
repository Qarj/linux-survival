# Kubernetes

## Install minikube

https://minikube.sigs.k8s.io/docs/start/

```sh
cd $HOME/Downloads
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube_latest_amd64.deb
sudo dpkg -i minikube_latest_amd64.deb
.
Setting up minikube (1.32.0-0) ...
```

## Start cluster

```sh
minikube start
.
😄  minikube v1.32.0 on Ubuntu 22.04
✨  Automatically selected the docker driver. Other choices: qemu2, virtualbox, none, ssh
📌  Using Docker driver with root privileges
👍  Starting control plane node minikube in cluster minikube
🚜  Pulling base image ...
💾  Downloading Kubernetes v1.28.3 preload ...
    > gcr.io/k8s-minikube/kicbase...:  453.90 MiB / 453.90 MiB  100.00% 43.54 M
    > preloaded-images-k8s-v18-v1...:  403.35 MiB / 403.35 MiB  100.00% 37.29 M
🔥  Creating docker container (CPUs=2, Memory=7900MB) ...
🐳  Preparing Kubernetes v1.28.3 on Docker 24.0.7 ...
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
🔗  Configuring bridge CNI (Container Networking Interface) ...
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🌟  Enabled addons: storage-provisioner, default-storageclass
💡  kubectl not found. If you need it, try: 'minikube kubectl -- get pods -A'
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
```

## Download appropriate version of kubectl

```sh
minikube kubectl -- get po -A
.
    > kubectl.sha256:  64 B / 64 B [-------------------------] 100.00% ? p/s 0s
    > kubectl:  47.56 MiB / 47.56 MiB [------------] 100.00% 12.51 MiB p/s 4.0s
NAMESPACE     NAME                               READY   STATUS    RESTARTS       AGE
kube-system   coredns-5dd5756b68-v28rg           1/1     Running   0              110s
kube-system   etcd-minikube                      1/1     Running   0              2m3s
kube-system   kube-apiserver-minikube            1/1     Running   0              2m5s
kube-system   kube-controller-manager-minikube   1/1     Running   0              2m3s
kube-system   kube-proxy-gn7gq                   1/1     Running   0              111s
kube-system   kube-scheduler-minikube            1/1     Running   0              2m3s
kube-system   storage-provisioner                1/1     Running   1 (109s ago)   2m2s
```

## Setup kubectl alias in `.bashrc`

```sh
alias kubectl="minikube kubectl --"
```

Start new terminal

```sh
kubectl version
.
Client Version: v1.28.3
Kustomize Version: v5.0.4-0.20230601165947-6ce0bf390ce3
Server Version: v1.28.3
```

## Setup Dashboard and start browser in terminal

```sh
minikube dashboard
.
🔌  Enabling dashboard ...
    ▪ Using image docker.io/kubernetesui/metrics-scraper:v1.0.8
    ▪ Using image docker.io/kubernetesui/dashboard:v2.7.0
💡  Some dashboard features require the metrics-server addon. To enable all features please run:

	minikube addons enable metrics-server


🤔  Verifying dashboard health ...
🚀  Launching proxy ...
🤔  Verifying proxy health ...
🎉  Opening http://127.0.0.1:39007/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/ in your default browser...
Opening in existing browser session.
```

## Install Ingress Nginx on minikube

```sh
minikube addons enable ingress
.
💡  ingress is an addon maintained by Kubernetes. For any concerns contact minikube on GitHub.
You can view the list of minikube maintainers at: https://github.com/kubernetes/minikube/blob/master/OWNERS
    ▪ Using image registry.k8s.io/ingress-nginx/kube-webhook-certgen:v20231011-8b53cabe0
    ▪ Using image registry.k8s.io/ingress-nginx/controller:v1.9.4
    ▪ Using image registry.k8s.io/ingress-nginx/kube-webhook-certgen:v20231011-8b53cabe0
🔎  Verifying ingress addon...
🌟  The 'ingress' addon is enabled
```
