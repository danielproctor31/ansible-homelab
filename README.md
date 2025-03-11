# ansible-homelab

## Prerequisites

- Install [Ansible](https://www.ansible.com/) on your control machine (local computer)
- Ensure you have an ssh key setup

```bash
ssh-keygen
```


## Usage:

First run needs to be done as root with password login
```bash
ansible-playbook playbook.yml -i inventory -u root -k
```

Subsequent runs should be performed as the remote user with ssh
```bash
ansible-playbook playbook.yml -i inventory -u your_remote_user
```
