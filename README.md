# ansible-homelab

## Prerequisites

- Install [Ansible](https://www.ansible.com/) on your Control Machine (Your Local Computer)
- Setup remote user with NOPASSWD
```bash
echo "your_remote_user ALL=(ALL) NOPASSWD: ALL" | sudo tee /etc/sudoers.d/your_remote_user_nopasswd
```

## Usage:

- Create Inventory file `inventory`:

```toml
[ubuntu_servers]
your_server_ip_or_hostname
```

- Copy your public ssh key to server
**This is important as once the playbook has been executed you will no longer have password logon available**

```bash
ssh-copy-id your_remote_user@your_server_ip_or_hostname
```

- Save `ubuntu_setup.yml` in the same directory as the inventory file

- From the same directory run:
  
```bash
ansible-playbook ubuntu_setup.yml -i inventory -u your_remote_user
```
