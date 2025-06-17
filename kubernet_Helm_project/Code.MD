# Fast need Application Files Like 
https://github.com/rafaftahsin/ostad-devops-batch-2-app

# install Helm linux

$ curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 <br>
$ chmod 700 get_helm.sh <br>
$ ./get_helm.sh

# install Helm Windows 
choco install kubernetes-helm


# Check Helm Version
helm version

# Check All Services
kubectl get all

# cert-manager Helm repo linux
helm repo add jetstack https://charts.jetstack.io
helm repo update

# cert-manager Helm repo windows
helm repo add jetstack https://charts.jetstack.io <br>
helm repo update

# Install cert-manager with CRDs
helm install cert-manager jetstack/cert-manager \
  --namespace cert-manager \
  --create-namespace \
  --set installCRDs=true

# Verify it's installed
kubectl get pods -n cert-manager

# create Helm directory 
 helm create .helm

# on Template folder 
delete All Template files  <br>
open tempate delete all 
making some yml file 
namespace,deployment,service,ingress,issure


# Helm install
helm install k8s-class .helm <br>
helm install k8s-class .helm -n ashraful

# Upgrade the existing release
helm upgrade k8s-class .helm/ -n ashraful


# Install NGINX Ingress Controller
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx <br>
helm repo update <br> 

helm install ingress-nginx ingress-nginx/ingress-nginx --namespace ingress-nginx --create-namespace 

#check the NGINX service type
kubectl get svc -n ingress-nginx

# Check ingress-nginx And SVC
kubectl get pods -n ingress-nginx <Br>
kubectl get svc -n ingress-nginx <Br>

# Helm install with Namespace if problem
helm install ostd.app .helm --create-namespace -n ashraful

# Check All with namespace
kubectl get all -n ashraful

# Check issuer 
kubectl get issuer -n ashraful

# Check ingress
 kubectl get ingress -n ashraful

# Check SVC 
kubectl get svc -n ingress-nginx


# Check certificate
kubectl get certificate -n ashraful


# Delete namespace
kubectl delete namespace ashraful


# Patch the existing namespace with Helm metadata

kubectl label namespace ashraful app.kubernetes.io/managed-by=Helm
kubectl annotate namespace ashraful \
  meta.helm.sh/release-name=ostd.app \
  meta.helm.sh/release-namespace=ashraful

# Run this commend
helm install k8s-class .helm -n ashraful

# Problem face
helm install k8s-class .heml/ -n ashraful


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

### ingress yml file

apiVersion: cert-manager.io/v1 <br>
kind: Issuer <br>
metadata: <br> 
  name: letsencrypt-prod <br>
  namespace: {{.Values.nameOverride}} <br>
spec: <br>
  acme: <br>
    server: https://acme-v02.api.letsencrypt.org/directory <br>
    email: rafaftahsin@gmail.com <br>
    privateKeySecretRef: <br>
      name: letsencrypt-prod <br>
    solvers: <br>
      - http01: <br>
          ingress: <br>
            ingressClassName: nginx <br>



### services yml file 

apiVersion: v1 <br>
kind: Service <br>
metadata:<br>
  name: {{ .Values.appName }}-service<br>
  namespace: ashraful<br>
spec:<br>
  type: NodePort<br>
  selector:<br>
    app: {{ .Values.appName }}<br>
  ports:<br>
    - port: {{ .Values.servicePort }}<br>
      targetPort: {{ .Values.containerPort }} <br>


### deployment yml file 

apiVersion: apps/v1  <br>
kind: Deployment  <br>
metadata:  <br>
  name: {{ .Values.appName }}  <br>
  namespace: {{ .Values.nameOverride }}  <br>
  labels:  <br>
    app: {{ .Values.appName }}  <br>
spec: <br>
  replicas: {{ .Values.replicaNumber }} <br>
  selector: <br>
    matchLabels: <br>
      app: {{ .Values.appName }} <br>
  template: <br>
    metadata: <br>
      labels: <br>
        app: {{ .Values.appName }}  <br>
    spec:  <br>
      containers:   <br>
        - name: {{ .Values.appName }}  <br>
          image: "{{ .Values.image.repository }}:{{ .Values.image.tag }}"  <br>
          imagePullPolicy: {{ .Values.image.pullPolicy }}  <br>
          ports:  <br>
            - containerPort: {{ .Values.containerPort }}  <br>
              protocol: TCP  <br>
          env:  <br>
            - name: SECRET_KEY  <br> 
              value: {{ .Values.env.SECRET_KEY | quote }}  <br>
            - name: SOCIAL_AUTH_GOOGLE_OAUTH2_KEY  <br>
              value: {{ .Values.env.SOCIAL_AUTH_GOOGLE_OAUTH2_KEY | quote }}  <br>
            - name: SOCIAL_AUTH_GOOGLE_OAUTH2_SECRET  <br>
              value: {{ .Values.env.SOCIAL_AUTH_GOOGLE_OAUTH2_SECRET | quote }}  <br>
      restartPolicy: Always









