the WSL IP can change (after WSL or Windows restart)

```bash
hostname -I | awk '{print $1}'
# Then edit your hosts file
# and Add this ip to Windows hosts file (as Admin)
notepad C:\Windows\System32\drivers\etc\hosts
# Flush windows DNS
ipconfig /flushdns
```
or
```bash
# Within WSL
cat > ~/update-hosts-windows.sh << 'EOF'
#!/bin/bash
WSL_IP=$(hostname -I | awk '{print $1}')
echo "WSL IP: $WSL_IP"
echo ""
echo "Add this to Windows hosts file (as Admin):"
echo "C:\Windows\System32\drivers\etc\hosts"
echo ""
echo "$WSL_IP sentiment-api.local"
EOF

chmod +x ~/update-hosts-windows.sh
```