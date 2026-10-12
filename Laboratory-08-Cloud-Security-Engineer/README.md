# Mission 8: The Cloud Security Engineer — CloudNova Technologies

**Author:** Charlene Padin Lomboy (@getsumei03)
**Course:** CCM101 – Cloud Computing | College of Information Technology, UEP
**Environment:** KillerCoda Ubuntu Playground + Docker + UFW
**Date:** October 2026

## Mission Overview
A junior developer at CloudNova Technologies deployed a client web app on Ubuntu but left all network ports wide open. As the dispatched Cloud Security Engineer, I secured the live server using defense-in-depth: deployed `secure-web-app` (Nginx on port 8080), audited open ports, enforced UFW with Default Deny, and poked only two precise holes — SSH (22) for admins and 8080/tcp for users.

> Security is not a product you buy; it is a continuous process you maintain.

## Objectives
- Understand Attack Surface and Principle of Least Privilege (PoLP)
- Perform basic security audit of active ports with `ss`
- Configure UFW with Default Deny incoming / Allow outgoing
- Allow only SSH + 8080/tcp, block everything else
- Document firewall rules and best practices in Markdown
- Expand GitHub Cloud Computing Portfolio to 8 missions

## Repository Structure
```
Laboratory-08-Cloud-Security-Engineer/
├── README.md
├── security-audit-report.md
├── firewall-configuration.md
├── reflection.md
└── screenshots/
    ├── vulnerable-app-running.png
    ├── firewall-activated.png
    └── firewall-port-allowed.png
```

## Commands Executed
```bash
sudo docker run -d --name secure-web-app -p 8080:80 nginx
curl http://localhost:8080
ss -tulpn
sudo ufw allow ssh
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw enable
sudo ufw status verbose
sudo ufw allow 8080/tcp
sudo ufw status numbered
curl http://localhost:8080
```

## Skills Learned
- Host-based firewall thinking vs. perimeter-only security
- PoLP in practice: no open port without a business reason
- UFW rule ordering and why SSH must come before `enable`
- Port auditing, `curl` verification, and Markdown security documentation
- Portfolio discipline: commit per checkpoint with screenshot evidence
