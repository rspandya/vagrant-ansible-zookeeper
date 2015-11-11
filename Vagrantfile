# -*- mode: ruby -*-
# vi: set ft=ruby :

BOXES = [
  {
    :name => "node-1",
    :eth1 => "192.168.205.10",
    :mem => "256",
    :idx => "1"
  },
  {
    :name => "node-2",
    :eth1 => "192.168.205.11",
    :mem => "256",
    :idx => "2"
  }
]

Vagrant.configure(2) do |config|
  
  BOXES.each do |opts|
    config.vm.define opts[:name] do |config|
      config.vm.box = "hashicorp/precise64"
      config.vm.hostname = opts[:name]
      config.vm.network :private_network, ip: opts[:eth1]
      config.vm.synced_folder ".", "/vagrant_data", id: "vagrant-root", disabled: true

      config.vm.provider "virtualbox" do |vb|
        vb.customize ["modifyvm", :id, "--memory", opts[:mem]]
        vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
      end

      config.vm.provision "shell", inline: "apt-get update"
      
    end
  end 
end
