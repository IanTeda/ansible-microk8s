---
Title:   Ansible User
Summary: Setting up node for Ansible
Authors: Ian Teda
Date:    September 8, 2021
---
# Ansible

## Update default user password

With a fresh install of Ubuntu we need to login to the default account and update the password.

```bash
ssh ubuntu@<ip-address>
Current password: ubuntu
New password: <secret-password>
Retype new password: <secret-password>
```

## Add Ansible user

Ubuntu will force exit your ssh session, so you will need to log back in with the password set above. Following add the ansible user.

``` bash
ssh ubuntu@ubuntu
sudo adduser --quiet --shell /bin/bash -ingroup sudo ansible
exit
```

## Generate private/public key

If we don't have a generated private/public key, lets go ahead and generate them.

```bash
ssh-keygen -f ~/.ssh/ansible 
```

## Copy private key to the node

Lets copy the public key so Ansible can login without a password.

```bash
ssh-copy-id -f -i ~/.ssh/ansible.pub ansible@<ip-address>
```

## Add node to our host file

If you installed Ansible with [Brew](https://brew.sh/) host can be added to `/usr/local/etc/ansible/hosts. But to keep everything in the repository we can add nodes to the `./inventory/cluster-1/host.ini` file. 

ansible_host can be set to hostname or IP address if you have assigned static IP address for your nodes.

```ini
[master]
node-1 ansible_host=192.168.1.11 ansible_ssh_private_key_file=~/.ssh/ansible ansible_user=ansible hostname=node-1

[nodes]
node-2 ansible_host=192.168.1.12 ansible_ssh_private_key_file=~/.ssh/ansible ansible_user=ansible hostname=node-2

[cluster:children]
master
nodes
```

## Config Users

Final step in this stage is to configure the node users. Run the 00-users playbook. This playbook will:

1. Allow ansible user to execute sudo without password
2. Remove ansible account password login
3. Disable default ubuntu password
4. Create and configure a default user

Since we haven't configure Ansible to allow sudo without password, we are prompted for Ansible user password and the default user password.

The default user is set in `./inventory/cluster-1/group_vars/all.yml

```bash
ansible-playbook 00-users.yml -i inventory/cluster-1/hosts.ini --ask-become-pass
BECOME pass: <ansible-password>
Enter default user password: <secret_password>
```
 
Finish off by copying public key to the node server

```bash
ssh-copy-id -f -i ~/.ssh/id_rsa.pub <default_user>@<ip-address>
```