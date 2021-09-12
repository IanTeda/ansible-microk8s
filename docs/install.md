---
Title:   Micork8s Install
Summary: Install, joining and configuring Microk8s 
Authors: Ian Teda
Date:    September 8, 2021
---
# Microk8s Install

Install Microk8s by running the "02-microk8s.yml" playbook.

```bash
ansible-playbook 02-microk8s.yml -i inventory/cluster-1/hosts.ini
```

The playbook will:

1. Install Microk8s
2. Add ansible user to the microk8s group
3. Alias kubectl and helm
4. Copy the .kube/config file to the local user
5. Join all the nodes to the cluster
6. Enable Microk8s addons


### Copy Kube Config

If you have more than one machine you can copy .kube/config file for local kubectl execution with the below SSH copy command

```bash
scp -i ~/.ssh/ansible ansible@node-1:~/.kube/config ~/.kube/config
```

## Install Apps

Install kubernetes apps by running the "03-apps.yml" playbook

```bash
ansible-playbook 03-apps.yml -i inventory/cluster-1/hosts.ini
```

The playbook will:

1. Ask what default database username should be. Default is "root"
2. Ask what the password for the default username should be. Default is "password"
3. Create a Postgres, Mongo and Redis databases with the default username and password.

_Note:_ If there are errors creating the apps you may need to create the subfolders "subPath" on the NFS server.