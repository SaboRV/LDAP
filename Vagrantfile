# -*- mode: ruby -*-
# vim: set ft=ruby :

MACHINES = {
  :ipa_otus_lan => {
        :box_name => "generic/centos8",
        :box_version => "4.3.12",
        :vm_name => "ipa.otus.lan",
        :net => [
                   {ip: '192.168.57.10', adapter: 2, netmask: "255.255.255.0"},

                ]
  },
  :client1_otus_lan => {
        :box_name => "generic/centos8",
        :box_version => "4.3.12",
        :vm_name => "client1.otus.lan",
        :net => [
                   {ip: '192.168.57.11', adapter: 2, netmask: "255.255.255.0"},
 
                ]
  },

  :client2_otus_lan => {
        :box_name => "generic/centos8",
        :box_version => "4.3.12",
        :vm_name => "client2.otus.lan",
        :net => [
                   {ip: '192.168.57.12', adapter: 2, netmask: "255.255.255.0"},

                ]
  },

}

Vagrant.configure("2") do |config|

  MACHINES.each do |boxname, boxconfig|
    
    config.vm.define boxname do |box|
   
      box.vm.box = boxconfig[:box_name]
      box.vm.host_name = boxconfig[:vm_name]
      box.vm.box_version = boxconfig[:box_version]

      config.vm.provider "virtualbox" do |v|
        v.memory = 4096
        v.cpus = 2
       end

      boxconfig[:net].each do |ipconf|
        box.vm.network("private_network", **ipconf)
      end

      box.vm.provision "shell", inline: <<-SHELL
        mkdir -p ~root/.ssh
        cp ~vagrant/.ssh/auth* ~root/.ssh
      SHELL
    end
  end
end

