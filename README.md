# slamp. #
Ansible playbook for LAMP+Solr intended for Drupal

## Prerequisites ##
[Install Vagrant](http://www.vagrantup.com/)
[Install Ansible](http://docs.ansible.com/intro_installation.html#installation)

## Install roles ##
Run the following to install required roles:
```
ansible-galaxy install -i -r requirements.txt
```

## Configure Shared Folder ##
An NFS share is configured in the Vagrantfile. Either create an empty folder in ```~/Sites/slamp``` or configure your desired folder location in the following line:
```
config.vm.synced_folder "~/Sites/slamp", "/var/www", type: "nfs"
```

## Configure /etc/hosts ##
Add entries to ```/etc/hosts`` for each site:
```
192.168.50.6  site1.local
192.168.50.6  site2.local
```