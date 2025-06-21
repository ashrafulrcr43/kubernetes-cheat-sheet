# Requirements 
1. minikube 
2. kubectl

## Install Argo CD
kubectl create namespace argocd 

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

## user And Password
user: admin
### password 
kubectl get secret argocd-initial-admin-secret -n argocd -o yaml <br>
echo N3BPQWFBLVJQTUk3N3VLSA== | base64 --decode



