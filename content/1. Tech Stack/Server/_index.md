+++
title = 'Server'
date = 2024-02-10T09:08:51Z
draft = false
tags = ["back end", "security"]
+++
## Overview

![Server Neofetch output](/images/server_specs.webp)

The server is running Debian 12 with half a gigabyte of ram and a CPU that can turbo around 2Ghz. This was chosen primarily because of cost constraints, however the resources available should be able to run a proof of concept project that can handle a small number of users without latency due to performance bottlenecks impacting the overall user experience. 

## Security measures

### RSA key authentication

Firstly, the server is configured only to accept logins with an RSA key and will not accept logins to the root account. This protects against brute force and credential stuffing attacks and ensures a user has the  minimum needed privileges when working on the server (the login non-root user can edit code and docker configuration but not system files).

### Fail2ban

The server is configured with fails2ban to ensure the server is as secure against brute force attacks as possible. A user has three attempts to submit the correct RSA key file; once they exceed this limit, their IP is placed in an "IP jail", and any further attempts to log in from their IP are ignored.

### Containerisation

As well as making the code base portable, the docker containers we use isolate each part of our program so any vulnerabilities or their dependencies aren't passed on to each other or the host system.
