For HPA -> HorizontalPodAutoscaler
scaling depending on CPU/RAM usage

```bash
# Install Metrics Server
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml

# For k3s, metrics-server may need insecure TLS
kubectl patch deployment metrics-server -n kube-system --type='json' \
  -p='[{"op": "add", "path": "/spec/template/spec/containers/0/args/-", "value": "--kubelet-insecure-tls"}]'

# Wait for metrics-server to be ready
kubectl get pods -n kube-system | grep metrics-server

# Test (wait 1-2 minutes for first metrics)
kubectl top nodes
kubectl top pods -n sentiment-app
```


```bash
# Create load testing pod 
kubectl run load-generator --image=busybox -n sentiment-app -- /bin/sh -c \ "while true; do wget -q -O- http://sentiment-api-service:8080/actuator/health; done"

# Watch HPA in another terminal 
kubectl get hpa -n sentiment-app -w 
# Watch pods scaling 
kubectl get pods -n sentiment-app -w
```