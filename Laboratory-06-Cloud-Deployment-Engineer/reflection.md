# Reflection — From Typing Commands to Writing Infrastructure

*Charlene Padin Lomboy — Lab 06*

Writing a `docker-compose.yml` felt like saving my work instead of redoing it every time. Before, I had to remember long `docker run` commands with ports, names, and passwords, and one typo meant starting over. Now everything lives in one file, so I just run `docker-compose up -d` and get the same Nextcloud plus MariaDB stack on any machine. If the university IT team asks how I did it, I do not recite commands from memory, I just send the file.

I learned the hard way that YAML hates tabs. I used a tab once in `nano` and Compose threw a mapping error and refused to start anything. Spaces are the only thing it accepts, usually two per level, because indentation is how it understands what belongs under `services:` or `environment:`. It was annoying at first, but it taught me to slow down and check alignment before running.

We used environment variables like `MYSQL_PASSWORD` so the images stay reusable. The same MariaDB image can become a different database just by changing variables, and Nextcloud knows which database to use without us editing its code. It also keeps credentials in one visible place instead of buried in commands.

Deploying Nextcloud in minutes honestly felt unreal. I expected enterprise storage to take hours, but after `up -d` and opening port 8080, there was the setup page. It made me feel like I could actually do deployment work, not just lab exercises.

Since Mission 1, my view changed a lot. I used to think cloud was just someone else's hard drive. Now I see it as layers: web tier, database tier, networks, and code that ties them together. I still get nervous with Linux, but `nano`, `ps`, and `down` finally feel familiar instead of foreign.
