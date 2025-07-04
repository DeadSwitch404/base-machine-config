# DeadSwitch Base Machine Configuration

**DeadSwitch | The Silent Architect**  
*"In silence, I rise. In storms, I endure."*  
---

##  What is this?

Two minimal yet powerful **Ansible playbooks** to deploy your base machine configuration for:

- **Debian-based systems** (Debian, Ubuntu)
- **RHEL-based systems** (RHEL, CentOS, Rocky, Alma)

DeadSwitch doesn't waste time. These playbooks are designed to be used **right after a fresh install**, before sudo is even configured. They assume one thing: **you came to control**.

---

## Features

**Core tasks included:**

- Install base packages (customizable list)
- Set static IP configuration
- Assign hostname and FQDN
- Create a user with **passwordless sudo**
- Deploy **authorized SSH keys**
- Tweak the shell prompt colors for easy role recognition (magenta = root, yellow = user)
- Final pause to confirm deployment status

**Debian playbook uses**:
- `apt`, traditional `/etc/network/interfaces` configuration

**RHEL playbook uses**:
- `dnf`, dynamic `nmcli` interface setup

---

## Requirements

- Ansible 2.15+
- Local machine with SSH access to target
- `--ask-become-pass` (uses `su` instead of sudo)

Install extra collections:

```bash
ansible-galaxy collection install community.general
```

## Usage

Clone the repo and adapt your inventory and variables:

```bash
ansible-playbook play-deploy-debian.yml -i inventory.ini --ask-become-pass
```

or

```bash
ansible-playbook play-deploy-redhat.yml -i inventory.ini --ask-become-pass
```

## Example Variables

group_vars:

```yaml
fqdn: "{{ hostname }}.yourdomain.com"
interface: enp1s0
gateway: 192.168.1.1
user: deadswitch404

packages:
  - mc
  - vim
  - curl
  - wget
  - sudo
  - tmux
```

host_vars:

```yaml
address: 192.168.1.200
hostname: deadmachine
```

## Philosophy

This is not a full OS hardening suite.  
This is the ghost’s bootstrapping ritual.  
A clean slate. An iron will. Ready to build or vanish.

## Audit or contribute?

All files are plain and human-readable. Fork. Review. Harden. Echo into the void.

    DeadSwitch operates where others hesitate.
    Share, fork, or forget—this code is open to the bold.

Fear the silence. Fear the switch.
