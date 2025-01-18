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
When I was renting in Vancouver, I had no access to my landlord's router that was connected to the ISP. I had a [Double NAT](https://kb.netgear.com/30186/What-is-double-NAT-and-why-is-it-bad) network, and could not publish any ports to the internet direcly. This lead me to utilze the [Cloudflare Zero Trust](https://developers.cloudflare.com/cloudflare-one/) suite of products, which could allow me to serve traffic through Cloudflare without access to a publicly routable IP address:
![Diagram showing how the Cloudflare Tunnel integrates with other product in the Zero Trust suite](/assets//img/posts/cloudflare.jpg){: width="972" height="589" .w-90 .normal}

The containers all currently reside on the Docker default [bridge network](https://docs.docker.com/engine/network/drivers/bridge/). A Cloudflare Tunnel (cloudflared) container that is deployed on that network, which creates outbound-only connections to Cloudflare's global network. Cloudflared is then configured to allow a public DNS records to reach private services on the bridge network:

```terraform
resource "cloudflare_tunnel_config" "servarr_tunnel" {
  config {
    ingress_rule {
      hostname = "plex.nathanjn.com"
      service  = "http://plex:32400"
    }
```

The Plex container is the only one that allows ingress traffic, as I wanted my TV, that can reach the host locally, to access content without going over the internet. The Plex container's port is mapped to the host, which allows for inbound private traffic to reach Plex:

```yaml
services:
  plex:
    ports:
      - 32400:32400
```

Most containers use the host's outbound internet connection. For containers that handle torrenting, they are attached to the Gluetun container's network, and use its VPN connection for outbound internet instead: 

```yaml
services:
  sonarr:
    network_mode: service:gluetun
    depends_on:
      - gluetun
```

## Monitoring
[Uptime Kuma](https://uptime.kuma.pet/) is a monitoring tool, which I use to monitor for HTTP(S) keyword and container states. 
Uptime Kuma is integrated with Pushbullet, and whenever a service is unavailable after two 60 second intervals, a push notification is sent to my phone:

![Push notification sent when there's service downtime](/assets/img/posts/push.png){: width="972" height="589" .w-50 .normal}


You can also use Uptime Kuma to publish a [service status dashboard](https://status.nathanjn.com/status/servarr), that is available for users:
 
![Uptime Kuma's service status dashboard](/assets/img/posts/status.png){: width="972" height="589" .w-90 .normal}
 


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
 - External monitoring
 - Network segmentation
 - Seamless SSH
 - NAS 
 - K8s 

