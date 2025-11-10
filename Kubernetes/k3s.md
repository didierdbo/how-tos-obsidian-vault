1. Description
	A light Kubernetes from Rancher, used in production
	
 
2. Installation
```bash
curl -sfL https://get.k3s.io | sh -
```
2. Configuration
```bash
mkdir -p ~/.kube 
sudo cp /etc/rancher/k3s/k3s.yaml ~/.kube/config 
sudo chown $USER:$USER ~/.kube/config
```
3. Check
```bash
kubectl get nodes
```
4. Stop
```bash
sudo systemctl stop k3s
```

```bash
# Check k3s service status
sudo systemctl status k3s

# Check k3s logs 
sudo journalctl -u k3s -n 50

# Stop k3s
sudo systemctl stop k3s
# Wait for complete
stop sleep 5

# Start k3s
sudo systemctl start k3s
sleep 15
kubectl get pods -n sentiment-app
sudo systemctl status k3s
```