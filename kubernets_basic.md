# fast Install docker,kubectl, minikube/kind I test Windows 
1. open WSL
2. OPen Docker
3. install minikube
Check kind-cluser folder 
# Check kubernets ns 
kubectl get ns
# Create new ns 
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

# Apply pods namespace 
kubectl apply -f create_pod.yml -n ashraful

# Check pod with namespace 
kubectl get pod -n ashraful
# Delete pods 
<pre>
  kubectl delete pod pod-name
  kubectl delete pod --all
</pre>
# Check Localhost on browser 
1. kubectl config set-context --current --namespace=ashraful
2. kubectl port-forward pod/nginx-pod 8080:80
3. http://localhost:8080
# Create deploymrnt.yml file 
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
# apply deployment file 
kubectl apply -f deployment.yml n ashraful
# check deployment and replica
1. kubectl get deployment -n ashraful
2. kubectl get pods
3. kubectl get pod -n ashraful
# delete deployment 
kubectl delete deployment <deployment-name>




   
