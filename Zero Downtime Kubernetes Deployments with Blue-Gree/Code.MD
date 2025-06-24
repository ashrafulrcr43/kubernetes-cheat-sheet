## I deploy this project 

# Chamge html File 
<h1>Hello from App Version 1</h1>

https://github.com/ashrafulrcr43/ostad-devops-batch-2-app
## Part 1: Create and Push Your Docker Image Version 1 
# Docker Image 
FROM node:18-alpine

WORKDIR /app
COPY . .

RUN npm install

EXPOSE 3000

CMD ["node", "index.js"]

## Make image and push 
docker build -t ashraful90/ostad-app:v1 . <br>
docker tag ashraful90/ostad-app:v1 ashraful90/ostad-app:v1 <br>
docker push ashraful90/ostad-app:v1 <br>
# Version 2 Change Html 
<h1>Hello from App Version 1</h1> 
<p>this is really version 1 <h1>

# make ersion 2 image 

docker build -t ashraful90/ostad-app:v2 . <br>
docker tag ashraful90/ostad-app:v2 ashraful90/ostad-app:v2 <br>
docker push ashraful90/ostad-app:v2 <br>

# Part 2 – Blue-Green Deployment
minikube start --driver=docker <br>
1. blue-deployment.yaml
2. green-deployment.yaml
3. service.yaml

## Apply YAML
kubectl apply -f blue-deployment.yaml
kubectl apply -f green-deployment.yaml
kubectl apply -f service.yaml

# Access App
minikube service myapp-service

# window Firewall 
1. security private = > off
2. inbound port allow

# Blue থেকে Green-এ সুইচ করুন
# Update service selector
kubectl patch service myapp-service -p '{"spec": {"selector": {"app": "myapp", "version": "green"}}}'

# Trabuleshot verify Endpoint
kubectl get endpoints ostad-app-service
1. if end point ip not found 
2. kubectl get svc ostad-app-service -o yaml
3. if sector not match 
selector:
    app: ostad-app-service
## edit service inline 
kubectl edit svc ostad-app-service
1. selector:
    app: ostad-app
## Finally check 
kubectl get endpoints ostad-app-service

## Then test it in the browser:
minikube service ostad-app-service



