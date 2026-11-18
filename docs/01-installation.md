# 01 - Ubuntu Server Installation

## Objective

Install and configure an Ubuntu Server virtual machine using Oracle VirtualBox on an Apple Silicon Mac, including initial system configuration, networking, and SSH setup.

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
2. Created a virtual machine in VirtualBox with 2 vCPUs, 2 GB RAM, and a 25 GB virtual disk.
3. Disabled unattended installation to configure Ubuntu manually.
4. Configured automatic networking using DHCP.
5. Installed Ubuntu Server using guided storage with LVM.
6. Created a non-root administrative user and configured the server hostname.
7. Installed OpenSSH Server and skipped optional server packages.
8. Verified the installation media was detached and booted from the virtual disk.
9. Updated system packages using `sudo apt update` and `sudo apt upgrade`.

## Initial System Verification

Verified the user, hostname, and operating system:

```bash
whoami
hostname
cat /etc/os-release
```

Confirmed:
- Username: `sysadmin`
- Hostname: `sudope`
- Operating System: Ubuntu Server 26.04.1 LTS

Updated installed packages:

```bash
sudo apt update
sudo apt upgrade
```

## Network Verification

Checked network interfaces and routing:

```bash
ip -br addr
ip route
```

Confirmed:
- Network interface: `enp0s8`
- IPv4 address: `10.0.2.15/24`
- Default gateway: `10.0.2.2`
- Network configuration: DHCP via VirtualBox NAT

Tested internet connectivity:

```bash
ping -c 4 google.com
```

**Result:** 4 packets transmitted, 4 received, 0% packet loss.

## SSH Configuration

Checked the SSH service:

```bash
sudo systemctl status ssh
```

Initially, the service reported `inactive (dead)`.

Enabled and started the SSH service:

```bash
sudo systemctl enable --now ssh
```

Verified that SSH was `active (running)` and listening on port 22.

Remote access from macOS will be configured in the next phase.

## Troubleshooting

### 1. Incorrect Installation File

**Issue:** Initially downloaded a `.iso.torrent` file, which macOS could not open.

**Resolution:** Downloaded the Ubuntu Server ISO directly instead of using the torrent file.

**Lesson:** Verify installation file types before configuring a virtual machine.

### 2. ARM64 Architecture Compatibility

**Issue:** Initially selected an AMD64 Ubuntu Server ISO, which was incompatible with the Apple M4 architecture.

**Resolution:** Downloaded the ARM64 ISO and configured VirtualBox to use Ubuntu (ARM 64-bit).

**Lesson:** Confirm that guest operating system architecture is compatible with the virtualization platform.

### 3. macOS Disk Image Error

**Issue:** macOS displayed "The disk image couldn't be opened" when attempting to open the Ubuntu ISO.

**Resolution:** Attached the ISO directly through VirtualBox rather than opening it in macOS.

**Lesson:** Operating system installation images can be mounted as virtual installation media.

### 4. Installation Media Removal

**Issue:** Ubuntu requested removal of the installation medium after installation, but the VirtualBox option was unavailable.

**Resolution:** Powered off the VM, opened VirtualBox storage settings, verified that the optical drive was empty, and restarted the VM.

**Lesson:** Virtual installation media is separate from the virtual hard disk containing the installed operating system.

### 5. SSH Service Inactive

**Issue:** The SSH service initially reported `inactive (dead)`.

**Resolution:** Enabled and started the service using:

```bash
sudo systemctl enable --now ssh
```

**Lesson:** Learned to inspect and manage Linux services using `systemctl`. An inactive SSH service can also be associated with socket activation, so service status should be interpreted alongside socket configuration.

## Outcome

Successfully deployed Ubuntu Server on an ARM64 virtual machine, configured storage and networking, updated system packages, verified internet connectivity, and enabled the SSH service.

The server is ready for remote access configuration and further Linux administration exercises.