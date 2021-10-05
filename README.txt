# 1-vm-enterprise

Template for a cloud edge CentOS 8 virtual workstation machine. 

It doesn't mean that you only have one VM, but only 1 VM on prem is required. Production runs elsewhere.

Run a private local VM that interacts other servers and with the internet to create and manage kubernetes and VMs deployed across the world.

CentOS 8 EPEL - "standard server" from CentOS 8 installer, gui or not, that will be modified by the scripts in this repo to use EPEL, docker, k3s, wazuh, and tuned for security and tooling. Doing a GUI for this device would be justified if the admins might want a web browser for accessing kibana or prometheus etc. Or perhaps just for web searching etc. This is a workstation after all, not a server per se, so GUIs can make sense in many cases for this "edge workstation" concept. 

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
- nethogs
- iotop


Restricting access to cloud administrative features is critical. The idea is to design those services so that the administrative components have minimum required access to function. With selinux and firewalld, locally, and then other firewalls and controls on each cloud instance only allowing from the authorized hardened workstations.


I set mine to do automatic updates at 6 AM and reboot if it wants to to keep the kernel and glibc on latest. I'm currently running pure docker as well as k3 deployments locally on the workstation for local tinkering and problem solving, that is not connected to the prod or qa clouds. Then I'm using the terminal and firefox/tor/vpns on on the workstation itself to access cloud web apis and dashboards, browser interactions with cloud vendors and vps providers, etc. I work on restricting and firewalling between the workstion and production cloud, so that there are only functionally minimum allowed ways to access the prod cloud apis.


### Ansible deployment

# customize your files and configs as needed, then while in the dir with make-epel-workstation and the other files:

tar czvf build.tgz ./*

ansible-playbook -u root -i hosts.inventory make-epel-workstation.yml

## note that if your centos 8 image doesn't have python or the expected yum package, you will need to install those before the ansible run


#### Setting the lock

mv /var/tmp/hardening-module.lock /etc/hardening-module.lock

This will prevent the harden script from executing again until the /etc/hardening-module.lock file is removed.

#### Debian-based usage (WIP)

There is now  harden-vm-debian script that can be used on debian-based systems with ufw instead of firewalld.
Debian compatibility/compontents are a work in progress and will be added TBD.

Also see https://github.com/jpegleg/deb_hardener

