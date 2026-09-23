# Reflection — From Containers to Durable Storage

*Charlene Padin Lomboy — CCM101 Lab 05*

Lab 04 taught me containers die fast, and Lab 05 showed why that matters for data. A block volume acts like one hard drive bolted to one VM — great for databases needing low-latency rewrites, but terrible for millions of photos because you would constantly resize, reformat, and bottleneck on a single mount. Object storage flips the model: every image is an independent object with its own key and metadata in a flat bucket, reachable over HTTP. It scales horizontally, replicates by itself, and serves directly to the app, which is exactly what a photo feed needs.

Docker made MinIO almost boring to install, in a good way. Instead of downloading binaries, creating users, and opening firewall rules by hand, one `docker run` with two `-p` flags and two `-e` flags gave me API on 9000 and UI on 9001 with a known admin login. I already knew `ps`, `stop`, and `rm` from Nginx, so `logs --tail` was the only new trick to confirm the server printed its WebUI URL. Rebuilding from scratch takes seconds, which encourages experimenting without fear.

I now picture a bucket as a giant labeled bin in the cloud with no real folders — just keys that look like paths. You PUT an object, MinIO stores bytes plus metadata and returns a key, and anyone with permission GETs it back via S3 API or browser. Versioning and policies sit on top of that simple primitive.

I assume enterprises survive crashes by never trusting one disk: MinIO erasure coding spreads shards across drives and nodes, plus cross-region replication and versioned backups, so losing a physical server just triggers a rebuild from remaining pieces. My Linux confidence also jumped — `docker ps`, reading logs, mapping ports, and using the Ports tab to reach 9001 no longer feels like magic. My portfolio now links theory in Lab 04 to stateful reality in Lab 05, which feels like actual data-engineering progress rather than just notes.


