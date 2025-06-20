
# Check namespace 
kubectl get ns     
# Create ns app
kubectl create ns app
# Apply deploymrnt & servoces 
kubectl apply -f deployment.yml <br>
kubectl apply -f service.yml <br>
 # Check service
kubectl get svc -n app     
# Check pods
kubectl get pods -n app



