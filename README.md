# ansible-desktop-playbook

## Prerequisites

Install [Ansible](https://www.ansible.com/) on your Control Machine (Your Local Computer)

## Usage:

- Create Inventory file `inventory`:

```toml
[ubuntu_servers]
your_server_ip_or_hostname
```

- Copy public key to server (if using ssh keys)

```bash
ssh-copy-id your_remote_user@your_server_ip_or_hostname
```

- Save `ubuntu_setup.yml` in the same directory as the inventory file

- From the same directory run:
  
```bash
ansible-playbook ubuntu_setup.yml -i inventory -u your_remote_user
```
