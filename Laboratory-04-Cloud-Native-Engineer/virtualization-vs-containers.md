# VMs vs Containers — Client Primer

*Charlene Padin Lomboy — CCM101 Laboratory 04 — Prepared for CloudNova client*

Our client asked why their VMs feel slow and heavy on RAM. Below is the simplest way I can explain the difference after my own testing.

## Side-by-Side Comparison

| What to Compare | Traditional Virtual Machine | Docker Container |
|---|---|---|
| **How it's built (Architecture)** | Hypervisor sits on hardware, then each VM boots its own complete Guest OS + libraries. App runs on top of that Guest OS. | Docker Engine sits on the Host OS. Containers share the host kernel and only bundle the app + needed libraries. No extra Guest OS. |
| **How fast it starts (Boot Time)** | Slow — usually 2 to 5 minutes. It has to power on a whole OS like a real computer. | Fast — usually 2 to 8 seconds. It just starts one isolated process because the OS is already running. |
| **How much it consumes (Resource Efficiency)** | Heavy. One VM easily eats 2GB+ RAM and 15GB+ disk for the OS alone. You can only fit a few VMs on one server. | Light. An Nginx image is around 180MB. You can run tens or even hundreds of containers on the same machine that struggles with 3 VMs. |
| **How isolated it is (Isolation Level)** | Hardware-level. Each VM has its own kernel, so if one crashes or gets compromised, others are well protected. Stronger but heavier. | Process-level. Linux namespaces + cgroups separate processes, network, and files. Very good for most web apps, but since the kernel is shared, isolation is lighter than a VM. |

## My Recommendation in Plain Words

If your workload is a standard web app like Nginx, staying on full VMs means you keep paying for idle operating systems that take minutes to boot and waste gigabytes of RAM. With containers you ship the same app in a small portable image that starts in seconds, uses far less memory, and behaves the same on your laptop and in the cloud. That is why I suggest moving the web tier to Docker first while keeping VMs only where you truly need a separate kernel. You will deploy faster, scale cheaper, and your IT team can reproduce my demo with three commands.

*Demo evidence: see `screenshots/docker-version.png`, `nginx-running.png`, `container-lifecycle.png`.*
