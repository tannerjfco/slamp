# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # All Vagrant configuration is done here. See: vagrantup.com.

  # Build against Ubuntu 12.04, without any config management utilities.
  config.vm.box = "ubuntu1204"
  config.vm.box_url = "http://puppet-vagrant-boxes.puppetlabs.com/ubuntu-server-12042-x64-vbox4210-nocm.box"

  # Enable host-only access to the machine using a specific IP.
  config.vm.network :private_network, ip: "192.168.50.6"

  # Provider-specific configuration for VirtualBox.
  config.vm.provider :virtualbox do |v|
    v.customize ["modifyvm", :id, "--name", "slamp"]
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--memory", 512]
    v.customize ["modifyvm", :id, "--cpus", 2]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  # Provisioning configuration for Ansible.
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
    ansible.inventory_path = "provisioning/inventory"
    # Run commands as root.
    ansible.sudo = true
    # Log/Debug Verbosity
    ansible.verbose = 'v'
    # Ensure host key checking disabled to prevent connection problems.
    ansible.host_key_checking = false
    # ansible.raw_arguments = ['-v']
  end

  # Setup NFS share
  config.vm.synced_folder "~/Sites/slamp", "/var/www", type: "nfs"
  config.nfs.map_uid = Process.uid   
  config.nfs.map_gid = Process.gid 

  # Set the name of the VM. See: http://stackoverflow.com/a/17864388/100134
  config.vm.define :slamp do |slamp|
    slamp.vm.hostname = "slamp"
  end

end