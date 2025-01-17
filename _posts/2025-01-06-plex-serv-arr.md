---
title: Plex serv[arr]
description: A media server that's secure, reliable, and hybrid cloud
date: 2025-01-06 15:00 +1000
tags: [cloudflare, terraform]
image:
  path: /assets/img/posts/servarr.png
  alt: An architecture diagram of the servarr soltuion
---





[Architecture Haiku](https://www.neverletdown.net/2015/03/architecture-haiku.html)


# Top attributes
## 

# Key attributes
- 

# Components
## Networking
Cloudflare Tunne;

For containers that handle torrenting, they are configured to use the Gluetun container for outbound traffic. 
All sensitive internet traffic is then routed through AirVPN, so that  
## Monitoring
Uptime Kuma


Plex server app

## Backups
Kopia The containers' configurations is automatically backed up to Cloudflare R2 

## Maintainability

IaC - Cloudflare, GitHub
CI/CD 

As the mounted disk has 8TB of space,  I use the Maintainerr container to automatically cleanup media that has been watched (or ignored) by the user who requested it. 


## Operations
The system is plug and play - all you need to do is provide the servarr with an ethernet connection and power, and on startup the drive is mounted and Docker is configured to start all the containers.

If and when a container exits unexpectedly, you can SSH into the servarr from a web browser and run a Docker command to bring it back up. 

When I want to onboard a new user, I use the Wizarr 

The Tautulli container is primarily used for monitoring Plex user data, but it can also be integrated with an SMTP relay to send newsletters when media has been recently added.
I've integrated Tautulli with SendGrid, but I use it for notifying to all users of any extended period of outages (e.g. when we move house). 


## Security
### Updates
I've installed Ubuntu Pro (22.04 LTS) on the servarr, and enabled Extended Security Maintainance (ESM).
A nightly cronjob then applies application security updates and kernel livepatching for high and critical CVEs.

The Watchtower container is used to automatically pull the latest images from the  

## Zero Trust
I've used Cloudflare as my Zero Trust solution...

## SSO
Google SSO for usability...

## Web application security
Any inbound traffic to the servarr is proxied by Cloudflare, which handles SSL certificates

## Cost



# Further work
 - Seamless SSH
 - NAS 
 - K8s 

