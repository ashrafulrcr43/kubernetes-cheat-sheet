# Requirements 
1. minikube 
2. kubectl

## Install Argo CD
kubectl create namespace argocd 

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

## port forward 
kubectl port-forward svc/argocd-server -n argocd 8080:443


## user And Password
user: admin
### password 
kubectl get secret argocd-initial-admin-secret -n argocd -o yaml <br>
echo N3BPQWFBLVJQTUk3N3VLSA== | base64 --decode

## making deployment,services,application files 
## push github 
## apply the application files
kubectl apply -f argocd-backend-app.yaml

# Check ArgoCD Server Pod Status






