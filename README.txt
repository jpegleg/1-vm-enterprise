# 1-vm-enterprise

Template for a cloud edge CentOS 8 virtual workstation machine. 

Run a private local VM that interacts other servers and with the internet to create and manage kubernetes and VMs deployed across the world.

CentOS 8 EPEL - server with GUI from install menu 

recommended min provisioning:
25 GB disk
4 vcores
8 GB RAM

recommended standard business provisioning:
150 GB disk
12 vcores
24 GB RAM

The idea is to have a single CentOS workstation that is used by the entire IT org as a shared resource: the system control station.
Production doesn't run on the workstation, but the workstation is allowed to spin up and down remote clouds, VMs, and services.
Collaborative tmux sessions can bring groups together, using selinux and firewalld as a team.

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
- tmux

Restricting access to cloud administrative features is critical. The idea is to design those services so that the administrative components have minimum required access to function. With selinux and firewalld, locally, and then other firewalls and controls on each cloud instance only allowing from the authorized secure workstations.
