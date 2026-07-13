# Ansible Lab Environment Setup

This guide explains how to prepare the control plane and managed nodes for an Ansible lab.

## Prerequisites

- Rocky Linux / RHEL / CentOS
- Root or sudo privileges
- Three virtual machines:
  - `control-plane`
  - `manage-node-1`
  - `manage-node-2`

---

# Step 1: Install Required Packages

Update the system:

```bash
sudo yum update -y
```

Install the required packages:

```bash
sudo yum install -y kernel-devel-$(uname -r)
sudo yum install -y kernel-headers dkms bzip2 make perl
```

> **Note:** If `kernel-devel` is not found, update the system and reboot before installing it.

---

# Step 2: Configure the Network

Create a new network connection on the control plane.

```bash
sudo nmcli connection add \
    con-name ansible-con \
    type ethernet \
    ifname eth2 \
    ipv4.method manual \
    ipv4.address 51.0.6.1/24 \
    ipv4.gateway 51.0.6.255
```

Bring the connection up:

```bash
sudo nmcli connection up ansible-con
```

Verify:

```bash
ip addr
```

---

# Step 3: Configure Hostname Resolution

Add the following entries to `/etc/hosts` on the control plane.

```text
51.0.6.1    control-plane
51.0.6.2    manage-node-1
51.0.6.3    manage-node-2
```

Or using commands:

```bash
echo "51.0.6.1 control-plane" | sudo tee -a /etc/hosts
echo "51.0.6.2 manage-node-1" | sudo tee -a /etc/hosts
echo "51.0.6.3 manage-node-2" | sudo tee -a /etc/hosts
```

---

# Step 4: Copy Hosts File to Managed Nodes

```bash
scp /etc/hosts root@manage-node-1:/etc/hosts

scp /etc/hosts root@manage-node-2:/etc/hosts
```

---

# Step 5: Install EPEL Repository

```bash
sudo yum install -y epel-release
```

---

# Step 6: Install Ansible

```bash
sudo yum install -y ansible
```

Verify the installation:

```bash
ansible --version
```

---

# Verify Connectivity

Test that all hosts are reachable.

```bash
ping manage-node-1

ping manage-node-2
```

---

# Environment Summary

| Host | IP Address |
|------|------------|
| control-plane | 51.0.6.1 |
| manage-node-1 | 51.0.6.2 |
| manage-node-2 | 51.0.6.3 |

---

Your Ansible control plane is now ready for inventory configuration and SSH setup.
