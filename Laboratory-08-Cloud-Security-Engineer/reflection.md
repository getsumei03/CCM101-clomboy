# Reflection — Thinking Like a Cloud Security Engineer

Joining the CloudNova Security Team for this mission changed how I view a “simple” Ubuntu server. Before, an open port felt harmless; now I see each one as an unpaid guard shift I have to staff forever.

A host-based firewall like UFW protects the server even if the perimeter is breached because it lives on the machine itself. Even if someone bypasses the VPC security group, office firewall, or KillerCoda network, UFW still inspects every packet at the host and drops anything not on its allow-list. That is defense in depth — I am no longer trusting one outer wall.

Managing open ports is how I shrink the attack surface. My audit with `ss -tulpn` showed SSH and 8080 listening to the world, which means automated bots can find them within minutes. By setting `default deny incoming` and allowing only 22 and 8080/tcp, I closed every door I did not consciously open. Fewer doors, fewer brute-force, exploit, and misconfiguration chances.

Leaving a database port like 3306 for MySQL open to the internet in a real enterprise would be catastrophic. Databases hold passwords, personal data, and payment records, and MySQL has a history of credential-stuffing and CVE exploits. Exposing it publicly invites ransomware, data exfiltration, and compliance violations; it should only be reachable from the app subnet or via VPN/bastion.

This mission made compromise feel terrifyingly easy. One forgotten `ufw enable` and one Nginx container is all it takes. Finally, with eight missions now, my portfolio `CCM101-clomboy` finally looks like a real engineer’s trail — from cloud concepts to Docker, Kubernetes, monitoring, and now security hardening — proof I can both build *and* protect in the cloud.
