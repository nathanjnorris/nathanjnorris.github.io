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


# Key attributes
  

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

## Backups
All containers store their configuration data within the */config* directory:

```yaml
services:
  wizarr:
    volumes:
      - /home/nathan/servarr/config/wizarr-config:/data/database
```

This is then mounted to Kopia as a read-only volume:

```yaml
services:
  kopia:
      volumes:
        - /home/nathan/servarr/config:/data:ro
```
A overnight backup of all container config is taken, then stored in Cloudflare R2 (S3-compatible storage), and retained according to a schedule.

## Maintainability

IaC - Cloudflare, GitHub
CI/CD 

As the mounted disk has 8TB of space,  I use the Maintainerr container to automatically cleanup media that has been watched (or ignored) by the user who requested it. 

## Monitoring
[Uptime Kuma](https://uptime.kuma.pet/) is a monitoring tool, which I use to monitor for HTTP(S) keyword and container states. 
Uptime Kuma is integrated with Pushbullet, and whenever a service is unavailable after two 60 second intervals, a notification is sent to my phone:

![Push notification sent when there's service downtime](/assets/img/posts/push.png){: width="972" height="589" .w-50 .normal}


I also use Uptime Kuma to publish a [service status dashboard](https://status.nathanjn.com/status/servarr) that is available for users:
 
![Uptime Kuma's service status dashboard](/assets/img/posts/status.png){: width="972" height="589" .w-90 .normal}
 
With a [Plex Pass](https://www.plex.tv/plex-pass/), you can use the [Plex Dash](https://play.google.com/store/apps/details?id=tv.plex.labs.dash&hl=en_NZ) app to monitor host metrics (bandwith, processor and memory) and any current user activity.

## Operations
The system is plug and play - all you need to do is provide the servarr with an ethernet connection and power. On boot, [fstab](https://www.redhat.com/en/blog/etc-fstab) is configured to mount the attached storage. Docker starts by default on Ubuntu, and all the containers are configured to always restart unless manually stopped:
```yaml
services:
  maintainerr:
    restart: always
```

If and when a container exits unexpectedly and cannot restart itself, you can SSH into the servarr from a web browser and run a *docker compose up -d* command to bring the container back to the correct state:

![SSH in a browser and starting a container that unexpectedly existed](/assets/img/posts/ssh.png)

SSH access via Cloudflare is restricted to either my Google identity, or an identity created for GitHub Actions. 
An attacker would need to compromise either of these identities, and the private key of a user on the servarr, in order to gain unauthorized access.

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

## User experience
When I want to onboard a new user to my Plex library and Overseerr I use the Wizarr app, which guides users on how to request media and on how to access the Plex client.

The Tautulli container is primarily used for monitoring Plex user data, but it can also be integrated with an SMTP relay to send newsletters when media has been recently added. I've integrated Tautulli with SendGrid, but I currently only use it for notifying to all users of any extended outages (e.g. when we move house). 



# Further work
 - External + metric monitoring
 - Network segmentation
 - Seamless SSH
 - NAS 
 - K8s 

