# Ansible playbook for Icinga2 on an Ubuntu 16.04
Ansible playbook for deploying an icinga2 server with Icingaweb2, Icinga2director, IDODB, Graphite and Grafana.

# About this ansible playbook
This ansible playbook applies some basicv roles, e.g. common, ssh-keys and webserver. The main role is the project-icinga role. This role is responsible for installing and configuring all icigna2 staff.

## commond role
The common role setups an ubuntu 16.04 maschine with some common settings, e.g.:
* disable ipv6
* install some basic tools: lsof, vim, nmap, iftop, htop, iotop, git, screen, tcpdump, pwgen etc.
* install openssh-server
* enabling ntp
* enabling unattended-upgrades
* setup rsylogd
* setup sudo 
* enabling etckeeper

## ssh-keys
The ssh-key role deploys ssh-keys to your maschine and to both users, the sudo user and the root user. The setting that you have to make to get the playbook running in your environment is described later.

## webserver role
The webserver role deploys a generic configured apache webserver with ssl enabled and as FQDN named vhosts. This role is implicit imported n the playbook via dependency, see roles/project-icinga/meta/main.yml.

## project-icinga role
The project-icinga role deploys all icinga2 components and their extra software, e.g. Grafana, Graphite, Icingaweb2, icinga2director etc.

# Get the playbook customized for your needs
* add hostname to "hosts" file
* change variables in group_vars/all
  - admin_user: change the name of the admin user that you want to use, must be changed in the playbook yml file too
  - admin_mail: change the mail address to your prefered mail address
  - add pubkey files as variable under "ssh-pubkeys:" 
* change variables in group_vars/icinga_maschines.yml to your needs
* SSH key deployment:
  - add ssh-pub-key as file in files/pubkeys/<USERNAME>.pub
  - copy/move host file in host_vars/icinga2.berkholz.org to host_vars/<FULLY_QUALIFIED_HOSTNAME>.yml 
  - add public key files for allowing or removing in file host_vars/<FULLY_QUALIFIED_HOSTNAME>.yml 
* change ntp server in roles/common/tasks/ntp.{{ ansible_distribution_release }}.yml
* change role/webserver/tasks/main.yml
  - apache ssl self signed certifiacte settings
* change ufw settings in roles/project-icinga/tasks/ufw.yml
  - change networks for http(s) connections
* change remote_user in main playbook yml file project-icinga_setup.yml to value of admin_user in group_vars/all 

