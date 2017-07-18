# ansible-icinga2-server
Ansible playbook for deploying an icinga2 server with Icingaweb2, Icinga2director, IDODB, Graphite and Grafana.

## Modifications to do:
* add hostname to "hosts" file
* change variables in group_vars/all
  - admin_user: change the name of the admin user that you want to use, must be changed in the playbook yml file too
  - admin_mail: change the mail address to your prefered mail address
  - add pubkey files as variable under "ssh-pubkeys:" 
* change variables in group_vars/icinga_maschines.yml to your needs
* SSH key deployment:
  - add ssh-pub-key as file in files/pubkeys/<USERNAME>.pub
  - copy/move host file in host_vars/icinga2.berkholz.org to host_vars/<FULLY_QUALIFIED_HOSTNAME>.yml 
  - add public key files for allowiung or removing in file host_vars/<FULLY_QUALIFIED_HOSTNAME>.yml 
* change ntp server in roles/common/tasks/ntp.{{ ansible_distribution_release }}.yml
* change role/webserver/tasks/main.yml
  - apache ssl self signed certifiacte settings
* change ufw settings in roles/project-icinga/tasks/ufw.yml
  - change networks for http(s) connections
* change remote_user in main playbook yml file project-icinga_setup.yml to value of admin_user in group_vars/all 

