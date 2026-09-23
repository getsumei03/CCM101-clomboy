# Reflection — What Containers Changed for Me

*Charlene Padin Lomboy — CCM101 Lab 04*

Before this lab my idea of deploying a website was installing a whole OS in VirtualBox, waiting for updates, then installing Nginx step by step. That easily eats half an hour and boots in minutes because the VM carries its own kernel and drivers. My Docker run felt unreal by comparison: one pull and one run command and Nginx answered in seconds. The speed gap comes from sharing the host kernel — containers skip the OS boot and just isolate the app process.

Port mapping finally clicked for me when I made a mistake. I first curled port 80 and got nothing, then remembered my container's port 80 is private inside Docker's network. Adding `-p 8080:80` builds a tunnel from my host's 8080 to that private 80, so `curl localhost:8080` actually reaches Nginx. Without publishing, the server runs but stays invisible, which is good default security but confusing until you see it fail once.

Deleting with `docker rm nginx-lab04` was also eye-opening. After removal `docker ps -a` went empty and everything I could have written inside vanished with the writable layer. That taught me to treat containers as throwaway: keep real data in volumes or images, never assume files inside survive a rebuild. It feels risky at first but forces cleaner habits.

For DevOps teamwork, I think this removes a lot of friction. Developers freeze dependencies into an image, operations runs that exact image anywhere, so the classic ours works but prod fails excuse fades. Both sides look at the same Dockerfile and run flags instead of long setup wikis. My previous labs were mostly concepts and comparisons, but this one gave me runnable proof with logs and screenshots. My portfolio now reads less like notes and more like I can actually ship and clean up a service, which is the shift from student to cloud-native thinking I wanted.

*Word count: ~310*
