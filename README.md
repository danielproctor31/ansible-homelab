# Ansible Homelab

Ansible playbook to configure and secure my homelab.

## Features

- 🔐 **Security hardening**: SSH, UFW firewall, Fail2ban
- 📦 **Automated updates**: Unattended security upgrades
- 🐳 **Docker**: Installation and configuration
- ⚙️ **System tuning**: Timezone, time sync, kernel parameters (swappiness)
- 👤 **User management**: Automated user setup with sudo access

## Supported Operating Systems

- **Debian**: 11 (Bullseye) and newer
- **Ubuntu**: 20.04 LTS and newer

## Prerequisites

1. **Install Ansible** on your control machine (local computer) [Install Ansible](https://docs.ansible.com/projects/ansible/latest/installation_guide/intro_installation.html)

2. **Set up SSH key** for authentication
   ```bash
   ssh-keygen
   ```

## Configuration

### 1. Update Inventory

Edit the [`inventory`](inventory) file with your server details:
```ini
[homelab_servers]
server1 ansible_host=192.168.1.100
server2 ansible_host=192.168.1.101
```

### 2. Customize Variables

Edit [`group_vars/homelab_servers.yml`](group_vars/homelab_servers.yml) to set:
- Username and SSH public key
- Timezone
- UFW allowed ports
- Other customizations

## Usage

### Running the Playbook

#### First Run (with password authentication)
```bash
ansible-playbook playbook.yml -i inventory -u your_remote_user -k -K
```
- `-k` prompts for SSH password
- `-K` prompts for sudo password

#### Subsequent Runs (with SSH key)
```bash
ansible-playbook playbook.yml -i inventory -u your_remote_user -K
```

### Dry Run (Check Mode)

Preview changes without making them:
```bash
ansible-playbook playbook.yml -i inventory --check
```

Combine with diff mode to see what would change:
```bash
ansible-playbook playbook.yml -i inventory --check --diff
```

### Using Tags

Run specific parts of the playbook:

```bash
# Only configure security settings
ansible-playbook playbook.yml -i inventory --tags security

# Only install Docker
ansible-playbook playbook.yml -i inventory --tags docker

# Multiple tags
ansible-playbook playbook.yml -i inventory --tags "security,docker"

# Skip package upgrades
ansible-playbook playbook.yml -i inventory --skip-tags upgrade
```

**Available tags:**
- `packages` - Package installation and management
- `initial` - Initial package installation
- `upgrade` - System package upgrades
- `user` - User creation and configuration
- `security` - All security-related tasks
- `system` - System configuration (timezone, time sync, sysctl)
- `time` - Time and timezone configuration
- `sysctl` - Kernel parameter tuning
- `docker` - Docker installation
- `updates` - Unattended upgrades configuration
- `ssh` - SSH hardening
- `fail2ban` - Fail2ban setup
- `firewall` - UFW firewall configuration
- `cleanup` - Package cleanup tasks

### Useful Ansible Commands

#### Test Connectivity
```bash
ansible all -i inventory -m ping
```

#### Run Ad-Hoc Commands
```bash
# Check disk space
ansible all -i inventory -a "df -h"

# Check system uptime
ansible all -i inventory -a "uptime"

# Reboot servers
ansible all -i inventory -a "reboot" --become
```

#### Verbose Output
```bash
# Show detailed output (-v, -vv, -vvv, -vvvv for increasing verbosity)
ansible-playbook playbook.yml -i inventory -v

# Debug level output
ansible-playbook playbook.yml -i inventory -vvv
```

#### Limit to Specific Hosts
```bash
# Run on only one server
ansible-playbook playbook.yml -i inventory --limit server1

# Run on multiple specific servers
ansible-playbook playbook.yml -i inventory --limit "server1,server2"
```

#### List Tasks and Tags
```bash
# List all tasks that would be executed
ansible-playbook playbook.yml -i inventory --list-tasks

# List all available tags
ansible-playbook playbook.yml -i inventory --list-tags

# List all hosts
ansible-playbook playbook.yml -i inventory --list-hosts
```

#### Step Through Tasks
```bash
# Prompt before each task
ansible-playbook playbook.yml -i inventory --step
```
## License

See [LICENCE](LICENCE)
