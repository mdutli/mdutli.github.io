---
title: Installing a second Router in my Network
summary: A slightly chaotic router setup that still ended in Pi-hole ad blocking.
tags:
  - networking
  - pihole
  - dhcp
  - homelab
---

## Goals

- Route my network traffic through Pi-hole to block ad domains.
- Use a more capable router with better Wi-Fi coverage.

## Why Change the Setup?

- My ISP router had limited configuration.
- I wanted ad blocking at the network level.
- The ISP router UI was painfully slow.

## Before and After

Before:

![Before diagram]({{ "/assets/26-01-11-dhcp-and-pihole/network-before.svg" | relative_url }})

After:

![After diagram]({{ "/assets/26-01-11-dhcp-and-pihole/network-after.svg" | relative_url }})

## Constraints I Hit

- The ISP router could not set a custom DNS server, so a simple Pi-hole setup would not work.
- The ISP router had no bridge mode, so I was not sure a second router would even function behind it.

## First Attempt and Failure

1. Plugged in a second router (named it goat-router), the ISP router of course detected it and gave it an IP.
2. Wanted the cleanest approach with no second DHCP Sever on the ISP router.
3. Moved all via LAN connected clients to goat-router (physically)
4. Moved all clients to the goat-router Wi-Fi.
5. Turned off Wi-Fi and DHCP on the ISP router.
6. Rebooted goat-router and immediately lost connection to the ISP router.

It turns out the ISP router still needed DHCP to give goat-router an IP. With
DHCP disabled, everything went dark.

![This is fine GIF]({{ "/assets/26-01-11-dhcp-and-pihole/this_is_fine.gif" | relative_url }})

## Recovery Steps

1. Plugged a client into the ISP router via LAN.
2. Set a manual IP on the client (network settings on Windows) in the ISP router subnet (I luckily knew by mind).
3. Logged into the ISP router at its default IP.
4. Restored settings without a full reset (phew).

## Second Attempt (After Losing Everything)

I kept DHCP enabled on both routers but separated them into different subnets.

1. ISP router subnet: 192.168.1.x, only the ISP router and goat-router live
   here.
2. Goat-router subnet: 192.168.2.x, goat-router at 192.168.2.1 and DHCP for all
   clients.
3. ISP router Wi-Fi stayed off, with a single LAN link to goat-router.
4. Clients moved to goat-router (kept the SSID to avoid reconfiguring devices).
5. Changed my password to a more secure one, so I had to do step 4 anyway (connect all devices)

This kept the network stable while avoiding a double-DHCP mess for clients.

## Pi-hole Setup

1. Ran Pi-hole on my home server using the official Docker image (no Raspberry Pi available).
2. Used macvlan so the container appears as a separate device on the network.
   Official docs: https://docs.docker.com/engine/network/drivers/macvlan/
3. Attached the container to my QNAP bridge and assigned it a fixed IP (also reserved on goat-router).
4. Set goat-router DNS to that Pi-hole IP.

Now every device connected to goat-router routes DNS through Pi-hole and blocks ad domains.

## Example Request Flow

![Example request flow]({{ "/assets/26-01-11-dhcp-and-pihole/request-flow.svg" | relative_url }})

## Takeaways

- Do not disable DHCP on the ISP router if it still needs to lease an IP to an upstream device.
- Separate subnets keep the ISP router happy while letting the second router own the client network.
- Pi-hole is easy to drop in once DNS control is on your side.
- CPU Usage high, might have reason to upgrade Home-Server now

![Pi-hole Dashboard]({{ "/assets/26-01-11-dhcp-and-pihole/pihole.png" | relative_url }})
