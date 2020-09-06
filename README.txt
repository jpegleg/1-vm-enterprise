# 1-vm-enterprise

Template for a cloud edge CentOS 8 virtual workstation machine. 

Run a private local VM that interacts other servers and with the internet to create and manage kubernetes and VMs deployed across the world.

CentOS 8 EPEL - server with GUI from install menu 

recommended min provisioning:
25 GB disk
8 vcores
8 GB RAM

recommended standard business provisioning:
150 GB disk
16 vcores
16 GB RAM

The idea is to have a single CentOS workstation that is used by the entire IT org as a shared resource: the system control station.

The vm and its files can be backed up every few hours ideally.

Software:

- k3s
- ansible
- cockpit
- docker
- SEC
- firewalld
- selinux
- clamd
- wazuh ossec manager
- git
- vim
