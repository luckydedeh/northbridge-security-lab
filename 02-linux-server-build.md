# 02 – Linux Server Build: lnx01

*Part of the Northbridge Financial Partners simulated security program. Lab environment, not production.*

## Objective

Deploy an Ubuntu server for Northbridge's internal services and apply baseline hardening: patching, role-based access, and a host firewall.

## Environment

- Host: MacBook Air (Intel), macOS
- Hypervisor: Canonical Multipass
- Guest OS: Ubuntu 24.04 LTS
- Resources: 2 vCPU, 2 GB RAM, 10 GB disk
- Hostname: `lnx01` | IP: `192.168.252.2`

## 1. Deployment

Launched the VM through Multipass and confirmed it was running:

```
multipass list
```

When the Multipass GUI shell failed to open, I connected from the macOS terminal instead:

```
multipass shell lnx01
```

## 2. Patch Management

```
sudo apt update && sudo apt upgrade -y
```

The upgrade installed kernel `6.8.0-142`, but the system was still running `6.8.0-139`, and needrestart flagged a pending reboot. I rebooted and verified the new kernel:

```
multipass restart lnx01
uname -r
# 6.8.0-142-generic
```

Result: 0 pending updates after the reboot.

## 3. Role-Based Groups and Users

Created security groups matching Northbridge's departments, then added users by role:

```
sudo groupadd hr
sudo groupadd finance
sudo groupadd sales
sudo groupadd it
sudo useradd -m -G finance jsmith
sudo useradd -m -G it adavis
```

Verified the membership:

```
id jsmith   # groups: jsmith, finance
id adavis   # groups: adavis, it
```

## 4. Host Firewall

Allowed SSH before enabling the firewall to avoid locking out remote access:

```
sudo ufw allow OpenSSH
sudo ufw enable
sudo ufw status
```

Result: the firewall is active and persists across reboots, with OpenSSH allowed over IPv4 and IPv6 and all other inbound traffic denied by default.


   ## Verification

   ![lnx01 kernel, user groups, and firewall status](screenshots/02-kernel-users-firewall.png)
   
## Lessons Learned

- Kernel updates don't take effect until a reboot, so verify the running version afterward.
- Allow SSH before enabling a firewall on a remote server, or you can lock yourself out.
- When a GUI tool fails, the CLI is often the more reliable path.

## Next Steps

- Switch SSH to key-based authentication and disable password login
- Forward logs to a central logging server (addresses the "no centralized logging" gap)
- Map these Linux groups to the Active Directory access model
