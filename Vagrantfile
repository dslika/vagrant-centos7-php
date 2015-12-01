# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "bento/centos-7.1"
  config.vm.box_check_update = false

  # config.vm.network :forwarded_port, guest: 80, host: 8000
  # using a specific IP.
  config.vm.network :private_network, ip: "192.168.33.33"
  config.vm.network :public_network, ip: "192.168.11.123", bridge: "en5: Thunderbolt Ethernet"

  config.vm.synced_folder "~/workspace/personalinfo", "/var/www/personalinfo", type: 'nfs'
  config.vm.synced_folder "~/workspace/daim_next", "/var/www/daim", type: 'nfs'

    config.vm.synced_folder "./share_data", "/share_data", :mount_options => ["dmode=777,fmode=775"]
    # :owner => "vagrant", :group => "vagrant",

    config.vm.provider "virtualbox" do |v|
      v.cpus = 2
      v.memory = 1024
      v.customize ["modifyvm", :id, "--natdnsproxy1", "off", "--natdnshostresolver1", "off", "--paravirtprovider", "kvm"]
    end


  # Enable provisioning with Ansible.
  config.vm.provision "shell", :path => "provision.sh"
  #config.vm.provision "ansible" do |ansible|
  #  ansible.playbook = "provisioning/site.yml"
  #  ansible.inventory_path = "provisioning/hosts"
  #  ansible.limit = 'all'
  #  ansible.verbose = 'vv'
  #end
end
