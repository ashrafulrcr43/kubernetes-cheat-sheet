# fast Install docker,kubectl, minikube/kind I test Windows 
1. open WSL
2. OPen Docker
3. install minikube
Check kind-cluser folder 
## Check kubernets ns 
kubectl get ns
## Create new ns 
kubectl crate ns ashraful
# making cluster 

# Create Pod with yml 
create_pod.yml:
<pre>
  apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod  
  labels:
    app: nginx      
spec:
  containers:
    - name: nginx-container
      image: nginx:latest
      ports:
        - containerPort: 80

</pre>

## Apply pods namespace 
kubectl apply -f create_pod.yml -n ashraful

## Check pod with namespace 
kubectl get pod -n ashraful
## Delete pods 
<pre>
  kubectl delete pod pod-name
  kubectl delete pod --all
</pre>
## Check Localhost on browser 
1. kubectl config set-context --current --namespace=ashraful
2. kubectl port-forward pod/nginx-pod 8080:80
3. http://localhost:8080
   
# Create deployment.yml file 
<pre>
  apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx

spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx-container
          image: nginx:latest
          ports:
            - containerPort: 80
  
</pre>
## apply deployment file 
kubectl apply -f deployment.yml n ashraful
# check deployment 
1. kubectl get deployment -n ashraful
2. kubectl get pods
3. kubectl get pod -n ashraful

## check replicaset 
kubectl get rs -n ashraful

## check browser -port-forward 
kubectl port-forward -n ashraful deployment/nginx-deployment 8080:80

## Run Background on Bash 
kubectl port-forward -n ashraful deployment/nginx-deployment 8080:80 &
## stop from Background run bellow comment bash
1. jobs
2. fg %1


## delete deployment 
kubectl delete deployment <deployment-name>

# making service for external world serve 
## Kubernetes Service Types 
1. ClusterIP (default)
=============================
### Use case: Internal communication inside the cluster.
### Behavior: Exposes the Service on a cluster-internal IP.
### Accessible: Only from inside the cluster.
2. NodePort
 =======================
### Use case: Simple external access (testing, dev).
### Behavior: Exposes the Service on a static port (the NodePort) on each cluster node’s IP.
## Accessible: From outside the cluster via http://<node-ip>:<node-port>.

3. LoadBalancer
   ==================================
### Use case: Production-grade external access (cloud environments).
### Behavior: Provisions an external load balancer from your cloud provider (AWS ELB, GCP LB, Azure LB, etc.).
### Accessible: From outside the cluster via the cloud LB’s external IP/DNS.

4. ExternalName
========================================
### Use case: Map a Kubernetes Service name to an external DNS name.
### Behavior: Returns a CNAME record to the client, effectively redirecting traffic to an external service.
### Accessible: Internal cluster name → external DNS name.
service.yml 
<pre>
  apiVersion: v1
kind: Service
metadata:
  name: nginx-service
  labels:
    app: nginx
spec:
  type: LoadBalancer
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 8080
      targetPort: 80
</pre>
## Apply Services 
kubectl apply -f service.yml -n ashraful
## Check service
kubectl get svc -n ashraful
## Delete Service
kubectl delete svc nginx-service -n ashraful




   
