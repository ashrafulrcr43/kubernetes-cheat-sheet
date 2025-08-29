
To install Docker In the Ubuntu System:

    sudo apt-get update
    sudo apt-get install docker.io -y
    sudo usermod -aG docker $USER && newgrp docker

Step 2:

- install Kind
- create a kind cluster with 2 worker node
- install kubectl

Step 3:
- make a deployment by kubectl apply -f app.yaml

Step 4:
- Install Helm
    curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3

    chmod 700 get_helm.sh

    ./get_helm.sh

 Step 5:

Install Prometheus

    helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

    helm repo add stable https://charts.helm.sh/stable

    helm repo update

    kubectl create namespace monitoring

    helm install kind-prometheus prometheus-community/kube-prometheus-stack --namespace monitoring --set prometheus.service.nodePort=30000 --set prometheus.service.type=NodePort --set grafana.service.nodePort=31000 --set grafana.service.type=NodePort --set alertmanager.service.nodePort=32000 --set alertmanager.service.type=NodePort --set prometheus-node-exporter.service.nodePort=32001 --set prometheus-node-exporter.service.type=NodePort

    kubectl get svc -n monitoring

    kubectl get namespace


Step 6:
- Forward The Port:

    kubectl port-forward svc/kind-prometheus-kube-prome-prometheus -n monitoring 9090:9090 --address=0.0.0.0


Step 7: 

-   Grafana Password
    - admin
    - prom-operator
