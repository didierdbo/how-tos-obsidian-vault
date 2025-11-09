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