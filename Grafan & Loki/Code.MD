# 1 .Deploy Fast

## Check namespace 
kubectl get ns     
## Create ns app
kubectl create ns app
## Apply deploymrnt & servoces 
kubectl apply -f deployment.yml <br>
kubectl apply -f service.yml <br>
 ## Check service
kubectl get svc -n app     
## Check pods
kubectl get pods -n app
## Run project 
kubectl port-forward svc/backend-service -n app 8000:8000
## Check browser 
http://localhost:8000/
# 2. Install Grafan & Loki
Grafan = Dashboard <br>
Loki = Log File




