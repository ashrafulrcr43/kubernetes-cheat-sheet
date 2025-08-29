# fast Install docker,kubectl, minikube/kind  
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
