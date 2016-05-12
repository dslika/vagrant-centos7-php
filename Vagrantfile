# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "centos7_php7"
  config.vm.box_check_update = false

  # config.vm.network :forwarded_port, guest: 80, host: 8000
  # using a specific IP.
  config.vm.network :private_network, ip: "192.168.33.33"
  config.vm.network :public_network, ip: "192.168.11.123", bridge: "en0: Ethernet"

  config.vm.synced_folder "~/workspace/personalinfo", "/var/www/personalinfo", type: 'nfs'
  config.vm.synced_folder "~/workspace/daim_next", "/var/www/daim", type: 'nfs'
  config.vm.synced_folder "./www-public", "/var/www/www-public", type: 'nfs'

  config.vm.synced_folder "./share_data", "/share_data", :mount_options => ["dmode=777,fmode=775"]

  config.vm.provider "virtualbox" do |v|
    # Chipset (Supposedly better CPU performance)
    v.customize [ "modifyvm", :id, "--chipset", "ich9" ]

    #CPU up to 4 cores and ioapic
    v.customize ["modifyvm", :id, "--ioapic", "on"]
    v.customize ["modifyvm", :id, "--cpus", "2"]
    v.customize ["modifyvm", :id, "--pae", "on"]
    v.customize ["modifyvm", :id, "--natdnsproxy1", "off"]
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "off"]
    v.customize ["modifyvm", :id, "--paravirtprovider", "kvm"]
    v.customize ["modifyvm", :id, "--memory", "4092"]

    v.customize ["setextradata", :id, "VBoxInternal/Devices/VMMDev/0/Config/GetHostTimeDisabled", 1]

    # SSD Settings
    v.customize ["storagectl", :id, "--name", "SATA Controller", "--controller", "IntelAHCI", "--portcount", "1", "--hostiocache", "on"]
    v.customize ["storageattach", :id, "--storagectl", "SATA Controller", "--port", "0", "--device", "0", "--nonrotational", "on"]
  end
end
