# ansible-homelab

Ansible playbook to configure and secure Debian and Ubuntu servers for homelab use.

## Supported Operating Systems

- Debian 11 (Bullseye) and newer
- Ubuntu 20.04 LTS and newer

## Prerequisites

- Install [Ansible](https://www.ansible.com/) on your control machine (local computer)
- Ensure you have an ssh key setup

```bash
ssh-keygen
```


## Usage:

### Configuration

Edit [group_vars/homelab_servers.yml](group_vars/homelab_servers.yml) to customize:
- Username
- Timezone
- UFW allowed ports

### Running the Playbook

First run needs to be done with password login
```bash
ansible-playbook playbook.yml -i inventory -u your_remote_user -k -K
```

Subsequent runs should be performed with ssh
```bash
ansible-playbook playbook.yml -i inventory -u your_remote_user -K
```

### Using Tags

Run specific parts of the playbook:
```bash
# Only configure security settings
ansible-playbook playbook.yml -i inventory --tags security

# Only install Docker
ansible-playbook playbook.yml -i inventory --tags docker

# Skip package upgrades
ansible-playbook playbook.yml -i inventory --skip-tags upgrade
```

Available tags: `packages`, `initial`, `upgrade`, `user`, `security`, `system`, `timezone`, `time`, `docker`, `updates`, `ssh`, `fail2ban`, `firewall`, `cleanup`
