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
## create namespace monitoring
kubectl create namespace monitoring
## Add Loki Helm repo
helm repo add grafana https://grafana.github.io/helm-charts <br>
helm repo update

## Install Loki Stack (Grafana + Loki + Promtail)
helm install loki-stack grafana/loki-stack \ 
  --namespace monitoring \
  --set grafana.enabled=true \
  --set promtail.enabled=true \
  --set loki.enabled=true

### This will install:
•	Loki <br>
•	Promtail (agent on each node to collect logs) <br>
•	Grafana (web UI) <br>

## Check pods
kubectl get pods -n monitoring

## Access Grafana Check fast
 kubectl get svc -n monitoring

##Expose Grafana Port forward Grafana
kubectl port-forward svc/loki-stack-grafana 3000:80 -n monitoring

## user and pass word
user : admin <br>

password:
kubectl get secret --namespace monitoring loki-stack-grafana -o jsonpath="{.data.admin-password}" | base64 --decode


## Configure Data Source in Grafana
1.	Go to Grafana → Settings (Gear icon) → Data Sources → Add data source
2.	Select Loki
3.	URL: http://loki-stack:3100
4.	Click Save & Test











