### Test resolution
```bash
nslookup google.com
```

### Detail DNS
```bash
dig google.com
```

### With specific server
```bash
dig @8.8.8.8 google.com
```

### Reverse lookup (IP → name)
```bash
dig -x 8.8.8.8
```

### Clear cache DNS local
```bash
sudo systemd-resolve --flush-caches
```