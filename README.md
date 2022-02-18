# k8s-prep
Kubernetes Prep

# Deploy nginx application
kubectl run nginx --image=nginx:alpine
kubectl run messaging --image=redis:alpine --labels=app=tier2

# Create a K8s NS
kubectl create namespace jagadeesh

kubectl get nodes -o json > nodes.json

# Create a service messaging-service to expose the messaging application within the cluster on port 6379.
#  Use imperative commands.
kubectl --expose pod messaging --name messaging-service --port 6379 --target-port 6379

# Create deployment with replicas
kubectl create deployment hr-web-app --image=nginx --replicas=2

# Create a static pod
kubectl run static-busybox --image=busybox -n kube-system --command sleep 1000 --dry-run=client -o yaml > static.yaml
copy to /etc/kubernetes/manifests
Kube-Scheduler should automatically create the static pod

# Create a service to existing deployment
kubectl expose deployment hr-web-app --name hr-web-app-service --type=NodePort --port 8080 --traget-port 8080 --dry-run=client -o yaml > svc.yaml
Manually add nodePort to the configuraiton after target port config

# Jsonpath syntax to dispaly only osiamges information for all nodes
kubectl get nodes -o jsonpath='{.items[*].status.nodeInfo.osImage}'
