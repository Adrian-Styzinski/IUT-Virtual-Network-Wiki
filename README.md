# Network Services Deployment: Nextcloud and OnlyOffice on Debian (Technical Wiki)

*Note: This wiki was originally written as a GitLab Wiki and imported here for archival, hence the absence of commit history. The project was done in pairs, and each of us wrote our own wiki, this repository contains mine.*

Technical wiki documenting the full deployment of a private cloud infrastructure on a virtualised two-subnet network running Debian. Completed in pairs for the S2.03 course "Installation de services réseaux" (BUT Informatique, IUT de Bordeaux), this is my own version of the documentation. It goes step by step from the network configuration to a working file-sharing and collaborative editing platform, with screenshots.

## Content and features

- **Virtual network (NEmu / QEMU):** Five Debian virtual machines (`router`, `ncloud`, `office`, `alice`, `bob`) split across two /24 subnets and connected by a router.
- **System and network configuration:** User management and sudo, dynamic then persistent static IP configuration (`/etc/network/interfaces`), IP forwarding and default gateways, connectivity tests with `ping`, `traceroute` and `ssh`.
- **Nextcloud server (via Snap):** Installation, HTTPS with a self-signed TLS certificate, two-factor authentication (TOTP with backup codes), password policy, groups and user accounts, shared folders and password-protected public links.
- **OnlyOffice document server:** Deployed on a dedicated machine, secured with a JWT secret and HTTPS, and connected to Nextcloud for in-browser document editing.
- **Nine Nextcloud plugins:** ONLYOFFICE, Splash, Passwords, Secrets, Draw.io, Calendar, FormVox, Notes and Talk, each documented with its purpose, installation and test procedure.
- **Client synchronisation:** Nextcloud Desktop client (apt or AppImage) installed on the client machines, with bidirectional synchronisation tested.
- **Command reference and portfolio:** Cheat sheet of the commands used (NEmu, network, users, APT, Snap, OCC) and an individual reflection on skills, challenges and lessons learned.

## Network architecture

| Subnet | Machines | Gateway |
|--------|----------|---------|
| Server LAN `192.168.1.0/24` | `ncloud` (.1), `office` (.2) | `router` eth0 (.254) |
| Client LAN `192.168.2.0/24` | `alice` (.1), `bob` (.2) | `router` eth1 (.254) |

The router's third interface (eth2) provides internet access to the whole infrastructure.

## Design choices

- **Snap instead of apt:** Nextcloud and OnlyOffice bundle many dependencies, so Snap packages (self-contained, sandboxed, auto-updated) make the installation simpler and less error-prone.
- **Dedicated OnlyOffice server:** Document processing is offloaded from the file server, as it would be in a professional environment.
- **Self-signed certificates:** All services are served over HTTPS, with the browser exception accepted manually.
- **Layered security:** HTTPS, TOTP two-factor authentication, password policy and protected sharing links.

## Skills demonstrated

Linux system administration (Debian), static and dynamic network configuration (IP addressing, routing, gateways), self-hosting services with Snap, HTTPS/TLS and access security, technical documentation in Markdown.

## Reading

The full wiki is in [`wiki_S2_03.md `](wiki_S2.03.md) (with a clickable table of contents), and its screenshots are in the `images/` folder.

```bash
git clone https://github.com/Chocopter/PU-Virtual-Network-Wiki
cd PU-Virtual-Network-Wiki
```