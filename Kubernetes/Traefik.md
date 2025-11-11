A Ingress controller included by defaul in k3s
```bash
# Check Traefik is running 
kubectl get pods -n kube-system | grep traefik
# Check Traefik service 
kubectl get svc -n kube-system | grep traefik

# Apply Ingress 
kubectl apply -f k8s/ingress/sentiment-api-ingress.yaml
# Check Ingress status 
kubectl get ingress -n sentiment-app
# Describe Ingress
kubectl describe ingress sentiment-api-ingress -n sentiment-app

# Add host entry (WSL) 
sudo bash -c 'echo "127.0.0.1 sentiment-api.local" >> /etc/hosts'
# Verify 
cat /etc/hosts | grep sentiment-api
```

curl http://sentiment-api.local/api/v1/analyze
    ↓
/etc/hosts resolve: sentiment-api.local → 127.0.0.1
    ↓
Traefik Ingress Controller (port 80)
    ↓
Ingress rule: host = sentiment-api.local
    ↓
Service: sentiment-api-service:8080
    ↓
Pod: sentiment-api
    ↓
Response: {"id":41, "sentiment":"POSITIVE"}

```bash
# Check Ingress details
kubectl get ingress -n sentiment-app

# Should show ADDRESS and HOSTS
kubectl describe ingress sentiment-api-ingress -n sentiment-app

# Check Traefik routing
kubectl logs -n kube-system -l app.kubernetes.io/name=traefik --tail=20
```
