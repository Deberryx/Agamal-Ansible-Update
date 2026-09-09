# Ubuntu Security Patching with Ansible

A small infrastructure-automation project created to standardize Ubuntu patching in a distributed public-health IT environment.

This repository is a **sanitized portfolio version** of the workflow. It contains no production credentials, public IP addresses, or organization-specific secrets.

## What the playbook does

The playbook targets Ubuntu servers in an Ansible inventory and:

- refreshes the APT package cache;
- performs a distribution upgrade;
- installs and enables `unattended-upgrades`;
- configures automatic security updates;
- checks whether Ubuntu has created `/var/run/reboot-required`;
- reboots only when the operating system reports that a reboot is required.

## Why I built it

Manual patching is repetitive and makes it harder to apply the same process consistently across Linux servers. I used Ansible to turn the patching workflow into a repeatable, auditable procedure that can be reviewed before execution and reused across hosts.

The project reflects the broader infrastructure work I do across Windows and Linux environments: automation, patch management, operational resilience, and reducing avoidable manual administration.

## Repository structure

```text
.
├── inventory.ini              # Sanitized example inventory
├── update-secure-ubuntu.yml   # Ansible playbook
├── LICENSE
└── README.md
```

## Requirements

- Ansible installed on the control host
- SSH access to the managed Ubuntu hosts
- A remote account permitted to use `sudo`
- Ubuntu 20.04 LTS or 22.04 LTS hosts, or a compatible Debian/Ubuntu environment after testing

## Example inventory

The committed inventory uses documentation-only addresses and should be replaced with your own hostnames or addresses in a private inventory.

```ini
[ubuntu_servers]
ubuntu-app-01 ansible_host=192.0.2.10
ubuntu-data-01 ansible_host=192.0.2.11
```

## Run the playbook

Start with Ansible connectivity validation:

```bash
ansible all -i inventory.ini -m ping
```

Review the target hosts:

```bash
ansible-inventory -i inventory.ini --graph
```

Then execute the playbook:

```bash
ansible-playbook -i inventory.ini update-secure-ubuntu.yml --ask-become-pass
```

In a production environment I would normally keep the real inventory, SSH configuration, vault material, and secrets outside a public repository.

## Operational considerations

Before using a patching playbook against production systems:

1. test against a non-production host;
2. confirm backups and recovery procedures;
3. review package changes and maintenance-window requirements;
4. use Ansible Vault or an external secret store rather than committing credentials;
5. execute against limited host groups first before broad rollout;
6. validate application and service health after patching.

## Skills demonstrated

`Ansible` · `Linux` · `Ubuntu` · `Infrastructure Automation` · `Patch Management` · `Security Updates` · `SSH` · `Operational Resilience`

---

**Author:** Derek Asamoah-Amoyaw  
Senior IT Infrastructure & Cloud Engineer · Microsoft Certified: Azure Administrator Associate (AZ-104)
