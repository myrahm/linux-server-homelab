# 01 - Ubuntu Server Installation

## Objective

Install and configure an Ubuntu Server virtual machine using Oracle VirtualBox on an Apple Silicon Mac.

## Environment

| Component | Configuration |
|---|---|
| Host | Apple M4 Mac, 16 GB RAM |
| Hypervisor | Oracle VirtualBox |
| Guest OS | Ubuntu Server 26.04.1 LTS (ARM64) |
| CPU | 2 vCPUs |
| Memory | 2 GB |
| Storage | 25 GB with LVM |
| Hostname | `sudope` |
| Username | `sysadmin` |
| Networking | NAT with DHCP |

## Installation Summary

1. Downloaded the Ubuntu Server ARM64 ISO.
2. Created a virtual machine in VirtualBox.
3. Configured CPU, memory, storage, and networking.
4. Installed Ubuntu Server using guided storage with LVM.
5. Created a non-root administrative user.
6. Configured the OpenSSH server during installation.
7. Removed the installation ISO and booted from the virtual disk.
8. Updated packages using `sudo apt update` and `sudo apt upgrade`.

## Verification

Verified the user, hostname, and operating system:

```bash
whoami
hostname
cat /etc/os-release
```

Tested internet connectivity:

```bash
ping -c 4 google.com
```

**Result:** 4 packets transmitted, 4 received, 0% packet loss.

## Troubleshooting

- **Architecture compatibility:** Replaced an AMD64 installation ISO with the ARM64 version required for Apple Silicon.
- **Installation media:** Verified the virtual optical drive was empty before rebooting the installed system.

## Outcome

Successfully deployed and updated an Ubuntu Server virtual machine with working network connectivity.