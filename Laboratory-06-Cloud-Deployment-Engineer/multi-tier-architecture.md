# Multi-Tier Architecture — Notes for the Client

*Charlene Padin Lomboy — Lab 06 — Why Nextcloud needs two containers*

A two-tier architecture just means we split the system into two parts that do different jobs but talk to each other. In our proof-of-concept, Tier 1 is Nextcloud and Tier 2 is MariaDB. The user only sees Tier 1, but Tier 1 cannot work without Tier 2 behind it.

## The Web / Application Tier

This is Nextcloud (`image: nextcloud`, mapped as `8080:80`).

Its role is everything the user touches: showing the login page, handling HTTP requests, uploading and listing files, sharing links, and checking permissions. When someone from the university opens port 8080, they are talking to this tier. It does not keep the important records itself — when a user logs in, this tier asks the database, "is this password correct?" and waits for the answer.

If this tier crashes, the site goes down but the data is still safe somewhere else, which is exactly why we separated them.

## The Database Tier

This is MariaDB (`image: mariadb:10.6`).

Its role is to remember things permanently: usernames and password hashes, file names, who owns what, share settings, and Nextcloud settings. In our Compose file we created `nextcloud_db` with user `nextcloud_user` for this purpose. Nobody browses to this container directly — it has no website port. It only listens for queries from the app tier inside the private Compose network.

I like to think of it as the back office. Students never walk in there, but without it the front desk cannot do anything.

## Why Separate Them?

Because they have opposite needs. The web tier needs to be replaced and updated often, while the database needs to stay stable and keep its data. If they were crammed into one container, updating Nextcloud could wipe the database, and a database problem could take down the whole image. Separate containers also let each part use the right image: Nextcloud's PHP-Apache setup for the web side, MariaDB's optimized engine for storage.

In short for our client: keeping the web server and database in two containers means we can restart or upgrade Nextcloud without touching student records, back up the database on its own schedule, and scale or fix one tier without breaking the other. It is cleaner, safer, and how real enterprise setups are done.
