# 🖥️ Linux Firewall Lab — Commands Used

This document lists all the commands executed during the `iptables` firewall configuration lab.  
Commands are grouped by purpose: system preparation, inbound rules, outbound rules, exceptions, and verification.  
Screenshots for each step are stored in the `images/` directory for documentation and audits.

```bash
# =========================
# System Preparation
# =========================
apt update              # Update package repositories
sudo -s                 # Switch to root shell
apt install iptables    # Install iptables firewall package
iptables --version      # Verify installation

# =========================
# Initial Firewall Status
# =========================
sudo iptables -L        # List current firewall rules

## Proof ##

![Initial Firewall Status Screenshot](Evidence/initial-firewall-status.png)


# =========================
# Inbound Rules
# =========================
iptables -A INPUT -p tcp -s 172.16.238.187 --dport 22 -j ACCEPT   # Allow SSH from trusted IP
iptables -A INPUT -p tcp -s 172.16.238.187 --dport 80 -j ACCEPT   # Allow HTTP from trusted IP
iptables -L -v                                                    # Verify active rules
iptables -A INPUT -j DROP                                         # Drop all other inbound traffic
iptables -L -v --line-numbers                                     # Verify with line numbers for audit

# =========================
# Outbound Rules
# =========================
iptables -A OUTPUT -p tcp -d 172.16.238.11 --dport 5432 -j ACCEPT   # Allow DB traffic
iptables -A OUTPUT -p tcp -d 172.16.238.15 --dport 80 -j ACCEPT     # Allow Repo server HTTP
iptables -A OUTPUT -p tcp --dport 80 -j DROP                        # Drop all other outbound HTTP
iptables -A OUTPUT -p tcp --dport 443 -j DROP                       # Drop all other outbound HTTPS
iptables -L -v --line-numbers                                       # Verify outbound rules

# =========================
# Exception Rule
# =========================
iptables -I OUTPUT -p tcp -d google.com --dport 443 -j ACCEPT       # Allow HTTPS only to Google
iptables -L OUTPUT -v --line-numbers                                # Verify OUTPUT chain rules

# =========================
# Audit Verification
# =========================
# Used iptables -L -v --line-numbers at different stages to confirm rule sets
# Screenshots stored in images/ directory for documentation and audits
