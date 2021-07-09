---
title: pg_dump via SSH Tunnel
date: 2021-06-30 10:00:00 +07:00
tags: [PostgresSQL, SSH]
description: This turned out to be simple, here are the two commands I used.
---
I've not had all that much experience with tunneling via SSH before, usually if I want to access a database I'm using something like _pgAdmin4_ so setting up an SSH tunnel by hand doesn't usually need to be done.

Today that changed for the first time, I wanted to dump some databases hosted on a server which required access via a tunnel. This turned out to be super simple, here are the two commands I used.

First, we setup a tunnel which connects my `localhost` port `5433` to the tunnel database hosts `5432`, I do this using the `-L` flag on the SSH command which allows me to bind a local port to a remote port. In the below command, __db-host__ is the host of my database, and tunnel-user@tunnel-host.com are the credentials for my tunnel server.

```bash
ssh -L localhost:5433:db-host:5432 tunnel-user@tunnel-host.com
```

That will open an SSH session which will stick around until killed, just like any other SSH session.

Once that's running, I can then open a new terminal on my machine and run the normal `pg_dump` command using the bound port.

```bash
pg_dump -f ~/Dekstop/db.sql -d postgres -h localhost -p 5433
```

That's it! Successful binding of a port to achieve tunneling for interacting with a postgres database via command line.