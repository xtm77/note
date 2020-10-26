# EKSCTL 설치
1. Chocolate 설치
https://chocolatey.org/install

```
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

```

## eksctl 설치
```
chocolatey install -y eksctl
chocolatey upgrade -y eksctl
eksctl version

```

https://github.com/weaveworks/eksctl/releases/download/0.23.0/eksctl_Windows_amd64.zip

## eks 클러스터 설치
```
eksctl create cluster --name admin13-cluster --version 1.15 --nodegroup-name standard-workers --node-type t3.medium --nodes 3 --nodes-min 1 --nodes-max 3
```

```
aws eks --region eu-west-1 update-kubeconfig --name admin13-cluster
kubectl config current-context
aws ecr get-login-password --region eu-west-1 | docker login --username AWS --password-stdin 052937454741.dkr.ecr.eu-west-1.amazonaws.com/admin13-procurementbook

docker login --username AWS -p $(aws ecr get-login-password --region ca-central-1) 052937454741.dkr.ecr.ca-central-1.amazonaws.com/
aws ecr get-login-password --region eu-west-1 | docker login --username AWS -p $(aws ecr get-login-password --region ca-central-1) 052937454741.dkr.ecr.ca-central-1.amazonaws.com/

kubectl create deploy admin13-procurementbook-1 --image="052937454741.dkr.ecr.eu-west-1.amazonaws.com/admin13-procurementbook:latest
"
kubectl expose deploy admin13-procurementbook-1 --type=ClusterIP --port=8086

```

```
choco install kubernetes-helm

사용자생성
kubectl --namespace kube-system create sa tiller 

kubectl create clusterrolebinding tiller --clusterrole cluster-admin --serviceaccount=kube-system:tiller
helm repo add stable https://kubernetes-charts.storage.googleapis.com/
helm repo update
kubectl create namespace ingress-basic
helm install nginx-ingress stable/nginx-ingress --namespace=ingress-basic

```

kubectl --namespace ingress-basic get services -o wide -w nginx-ingress-controller