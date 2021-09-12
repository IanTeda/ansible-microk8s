---
Title:   Ansible Microk8s
Summary: What this repository is all about
Authors: Ian Teda
Date:    September 8, 2021
---
# Ansible Microk8s

This documentation walks through setting up a Micok8s cluster on RaspberryPis using Anisble. It assumes you have cloned the git repository and have Ansible installed.

## What is this repository?

This repository is a collection of Ansible playbooks for setting 

This setup uses the Ubuntu Server 64bit OS. We want 64bit because the docker hub images are limited for 32bit.

## What is Ansible?

[Ansible](https://www.ansible.com/) is an open source community project sponsored by Red Hat, it's the simplest way to automate IT. Ansible is the only automation language that can be used across entire IT teams from systems and network administrators to developers and managers. Ansible is the most popular open source automation tool on GitHub today with more than a quarter million downloads per month.

## How is this repository structured

This repository goes through setting up the Ansible user on the node, then configuring the node and finally working with Microk8s

# References

* [Microk8s](https://microk8s.io/)
* [Ansible](https://www.ansible.com/)