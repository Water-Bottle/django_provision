# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "ubuntu/trusty64"
  config.ssh.forward_agent = true  # external SSH connections to use host keys

  config.vm.provider "virtualbox" do |v|
    v.memory = 1024
    v.cpus = 1
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  config.vm.define "waterbottle" do |waterbottle|
    waterbottle.vm.hostname = "waterbottle"
    waterbottle.vm.network "private_network", ip: "192.168.33.10"
    # waterbottle.vm.network "forwarded_port", guest: 8080, host: 8080
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provision/site.yml"
    ansible.inventory_path = "provision/hosts/vagrant"
    ansible.limit = "all"
    # ansible.verbose = "vvvv"
  end

end
