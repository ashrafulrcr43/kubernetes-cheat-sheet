
# install Helm 

$ curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 <br>
$ chmod 700 get_helm.sh <br>
$ ./get_helm.sh


# Check Helm Version
helm version

# Check All Services
kubectl get all

#create Helm directory 
helm create .helm

on Template folder 
making some yml file 
namespace,deployment,service,ingress,issure

# cert-manager Helm repo
helm repo add jetstack https://charts.jetstack.io
helm repo update

# Install cert-manager with CRDs
helm install cert-manager jetstack/cert-manager \
  --namespace cert-manager \
  --create-namespace \
  --set installCRDs=true

# Verify it's installed
kubectl get pods -n cert-manager

# Helm install
helm install k8s-class .helm
helm install k8s-class .helm -n ashraful

# Delete namespace
kubectl delete namespace ashraful


helm install ostd.app .helm --create-namespace -n ashraful

# Patch the existing namespace with Helm metadata

kubectl label namespace ashraful app.kubernetes.io/managed-by=Helm
kubectl annotate namespace ashraful \
  meta.helm.sh/release-name=ostd.app \
  meta.helm.sh/release-namespace=ashraful

# Run this commend
helm install k8s-class .helm -n ashraful

# Problem face
helm install k8s-class .heml/ -n ashraful


# Upgrade the existing release
helm upgrade k8s-class .heml/ -n ashraful

# Check if the NGINX Ingress
kubectl get pods -n ingress-nginx

# Add entry to your Windows host's hosts file
Open Notepad as Administrator.
C:\Windows\System32\drivers\etc\hosts

192.168.0.100   k8s-ashraful.rfft.nl


# Test directly via IP and NodePort
kubectl get svc -n ashraful


# NGINX Ingress Controller Exposing Port 80/443
kubectl get svc -n ingress-nginx

#check the NGINX service type
kubectl get svc -n ingress-nginx

#if not presend 
helm uninstall ingress-nginx -n ingress-nginx
helm install ingress-nginx ingress-nginx/ingress-nginx \
  --namespace ingress-nginx --create-namespace \
  --set controller.service.type=NodePort \
  --set controller.service.nodePorts.http=30080 \
  --set controller.service.nodePorts.https=30443


### port-forward command:
kubectl port-forward --address 0.0.0.0 svc/k8s-class-service 3000:8000 -n ashraful


# Now Change Helm Variable
## values files

repository: ashraful90/rapidcompetitions <br>
  pullPolicy: IfNotPresent  <br>
  tag: latest  <br>

  nameOverride: ashraful  <br>
  fullnameOverride: ashraful  <br>
  appName: k8s-class  <br>
  replicaNumber: 1  <br>
  containerPort: 8000  <br>
  servicePort: 8000  <br>

  env:
   SECRET_KEY: "hello_world"  <br>
   SOCIAL_AUTH_GOOGLE_OAUTH2_KEY: "776969788616-f4d7v9porfn30v1n52u2vlohi5s6kbvv.apps.googleusercontent.com"  <br>
   SOCIAL_AUTH_GOOGLE_OAUTH2_SECRET: "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"  <br>
   STRIPE_PUBLIC_KEY: "pk_test_51NKOdABvOW3ENPuKaMob7GBaX0qVXyBPiguf3Upc6kM19htAoRotDtPXXBooFc5z9kP5vvB16hXv6qXAdUCqiv6b00mAnDW10c"  <br>
   STRIPE_SECRET_KEY: "sk_test_51NKOdABvOW3ENPuK5FPCZDDYCpJKj0CqLibwctOrW3n6CNaBm0xIDBMlBCBWkpR8G5BZteemwBA3QZoMJfRw3bnZ00tYZkRoB8"  <br>

### namespace yml file
apiVersion: v1 <br>
kind: Namespace <br>
metadata: <br>
  name: {{.values.nameOverride}} <br>









