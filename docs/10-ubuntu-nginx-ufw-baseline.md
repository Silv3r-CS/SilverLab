# Ubuntu Nginx and UFW Baseline

## Objective

Deploy a lightweight internal web service on the Ubuntu Server VM and secure it with UFW firewall rules.

This milestone demonstrates Linux service deployment, web server configuration, firewall hardening, and network validation inside the SilverLab homelab.

## Environment

| Component | Details |
|---|---|
| VM | SilverServer-Ubuntu |
| Hostname | homelab-silver |
| IP address | 192.168.1.120/24 |
| Gateway | 192.168.1.1 |
| Hypervisor | Proxmox VE on Laptop 2 |
| Web service | Nginx |
| Firewall | UFW |

## Deployment Summary

Nginx was installed on the Ubuntu Server VM and configured to serve a custom internal SilverLab status page. UFW was enabled with a least-privilege baseline allowing only SSH and HTTP inbound traffic.

## Commands Used

| Command | Purpose |
|---|---|
| `sudo apt update` | Refresh package lists before installing software |
| `sudo apt install nginx -y` | Install the Nginx web server |
| `systemctl status nginx --no-pager` | Confirm Nginx is active and running |
| `curl -I http://127.0.0.1` | Test that Nginx responds locally |
| `sudo mkdir -p /var/www/silverlab` | Create a dedicated folder for the SilverLab web page |
| `sudo tee /var/www/silverlab/index.html` | Create the custom internal web page |
| `sudo tee /etc/nginx/sites-available/silverlab` | Create a dedicated Nginx site configuration |
| `sudo ln -sf /etc/nginx/sites-available/silverlab /etc/nginx/sites-enabled/silverlab` | Enable the SilverLab Nginx site |
| `sudo rm -f /etc/nginx/sites-enabled/default` | Disable the default Nginx welcome site |
| `sudo nginx -t` | Test Nginx configuration syntax before reload |
| `sudo systemctl reload nginx` | Apply the new Nginx configuration safely |
| `sudo ufw allow OpenSSH` | Allow SSH administration |
| `sudo ufw allow 'Nginx HTTP'` | Allow HTTP access to the web service |
| `sudo ufw enable` | Enable the UFW firewall |
| `sudo ufw status verbose` | Confirm firewall status and rules |

## Outcome

The Ubuntu Server VM now hosts a custom internal SilverLab web page at:

```text
http://192.168.1.120
