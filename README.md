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
2.  [Alert Manager](http://localhost:9093/)

## Contents

This will add a recommended set of monitoring rules to prometheus for Redis Enterprise clusters.

These rules are not all inclusive and some may need to be disabled or thresholds modified.

All alerts will contain a link to the runbooks.  Sample run books have been included separated by alert types and contain detailed information on what is being monitored and why


- [Capacity](./runbooks/capacity.md)
- [Connections](./runbooks/connections.md)
- [Latency](./runbooks/latency.md)
- [Nodes](./runbooks/nodes.md)
- [Shards](./runbooks/shards.md)
- [Utilization](./runbooks/utilization.md)
- [Throughput](./runbooks/throughput.md)
