---
Title:   Ubuntu Node Config 
Summary: Setting up Ubuntu server node
Authors: Ian Teda
Date:    September 8, 2021
---
# Ubuntu Server Node

To config Ubuntu server as a node we run the following playbook, referencing our `host.ini` file.

```bash
ansible-playbook 01-node.yml -i inventory/cluster-1/hosts.ini
```

The playbook will

1. Configure the Ubuntu server install
2. Secure SSH login
3. Update and install required apt packages
4. Setup and enable the firewall