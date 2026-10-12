# Firewall Configuration Log (UFW)

## 1. Allow SSH for Remote Administration
```bash
sudo ufw allow ssh
# Allows TCP 22 inbound. Ran FIRST to prevent lockout.
```

## 2. Set Default Deny Policy
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
# Inbound: dropped unless explicitly allowed.
# Outbound: allowed so server can apt update, pull Docker images, and respond.
```

## 3. Activate and Verify
```bash
sudo ufw enable
sudo ufw status verbose
# Expected: Status: active, Default: deny (incoming), allow (outgoing)
```

## 4. Allow Web Application Port 8080
```bash
sudo ufw allow 8080/tcp
sudo ufw status numbered
curl http://localhost:8080
# curl succeeds now because of this explicit hole.
```

## Critical Warning
If you run `sudo ufw enable` before `sudo ufw allow ssh`, you will instantly lock yourself out of your own server over SSH and require console/physical access to recover.
