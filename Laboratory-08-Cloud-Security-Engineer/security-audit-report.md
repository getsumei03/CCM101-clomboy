# Security Audit Report — CloudNova Vulnerable Server
**Engineer:** Charlene Padin Lomboy | **Host:** KillerCoda Ubuntu | **App:** secure-web-app (Nginx on 8080)

## 1. Security Best Practices (Chapter 8 - In My Own Words)

**The Principle of Least Privilege (PoLP):**
PoLP means giving a user, app, or service only the exact permissions it needs to do its job — nothing extra, and only for as long as needed. For cloud accounts, this is critical because if an over-privileged account gets phished or a key leaks, the attacker inherits all that extra power and can delete buckets, spin up miners, or steal databases.

**Attack Surface:**
When applied to a virtual machine, the attack surface is the total sum of all reachable entry points an attacker could try — open ports, running services, SSH logins, web routes, and even outdated packages. Every extra listening port on my Ubuntu server, like leaving 8080 or 3306 open to 0.0.0.0/0, is another door I have to guard.

**Default Deny Policy:**
Default Deny means the firewall blocks all incoming traffic automatically unless I explicitly create an allow rule for it. It is safer than blocklisting hackers one-by-one because I cannot possibly know every attacker IP or new exploit in advance, while I *do* know my app only needs ports 22 and 8080.

## 2. Baseline Audit
```bash
ss -tulpn
sudo docker ps --filter name=secure-web-app
curl -I http://localhost:8080
