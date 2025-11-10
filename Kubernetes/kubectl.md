1. Various useful commands
```bash

# Delete deployments/statefulsets only 
kubectl delete deployment ml-service -n sentiment-app
kubectl delete statefulset postgres -n sentiment-app
kubectl delete deployment api-service -n sentiment-app
# PVCs remain, data preserved
kubectl get pvc -n sentiment-app
# Still there

# Delete everything in namespace
kubectl delete namespace sentiment-app
# This removes: 
# - All pods 
# - All services 
# - All deployments/statefulsets 
# - All PVCs (data will be lost!)

kubectl apply -f k8s/ 
# Pods restart and reconnect to existing PVCs

# Verify data saved in PostgreSQL
kubectl exec -it postgres-0 -n sentiment-app -- psql -U postgres -d sentiment -c "SELECT * FROM analyses;"

# Check API logs
kubectl logs -f sentiment-api-584ff746f5-nnkxt -n sentiment-app
# Check logs of new pod
kubectl logs -f deployment/sentiment-api -n sentiment-app

# Port-forward API
kubectl port-forward -n sentiment-app svc/sentiment-api-service 8080:8080

# Deploy API deployment and service
kubectl apply -f k8s/api-service/
# Redeploy API on K8s
kubectl apply -f k8s/api-service/deployment.yaml

# Verify deployment
kubectl get deployments -n sentiment-app
# Check pods
kubectl get pods -n sentiment-app
# Verify
kubectl get pods -n sentiment-app -w
# Check pod environment variables
kubectl get pod sentiment-api-584ff746f5-nnkxt -n sentiment-app -o yaml | grep -A 20 env:
# See service details
kubectl get svc sentiment-api-service -n sentiment-app
# See which pods the service targets
kubectl get endpoints sentiment-api-service -n sentiment-app

# Force rollout restart
kubectl rollout restart deployment/sentiment-api -n sentiment-app
# Check deployment status
kubectl rollout status deployment/sentiment-api -n sentiment-app
# Check deployment config
kubectl describe deployment sentiment-api -n sentiment-app

# Import API image to k3s
docker save sentiment-api:v1 | sudo k3s ctr images import -
# Verify
sudo k3s ctr images ls | grep sentiment-api

# Delete only the API deployment
kubectl delete deployment sentiment-api -n sentiment-app
```


2. Scale to Zero
```bash
# Scale to 0 replicas 
kubectl scale deployment sentiment-api --replicas=0 -n sentiment-app 
# Verify 
kubectl get pods -n sentiment-app 
# sentiment-api pod disappears 
# Test locally... 
# Resume when done 
kubectl scale deployment sentiment-api --replicas=2 -n sentiment-app

kubectl cluster-info
```

