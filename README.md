# Monitoring Redis Enterprise with Prometheus

Example monitoring setup for Prometheus

## Pre-reqs

1. Ansible [installation](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
2. Vagrant [installation](https://www.vagrantup.com/downloads.html)

## Setup Data collection

1. copy ansible/vars/main.yml.example to ansible/vars/main.yml and edit the file
2. vagrant up --provision

## Views

1.  [Prometheus](http://localhost:9090/)
1.  [Alert Manager](http://localhost:9093/)