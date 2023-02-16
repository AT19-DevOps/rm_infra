# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  config.vm.provision :docker
  config.vm.define "server-1" do |dockerserver|
    dockerserver.vm.network "private_network", ip: '192.168.33.60'
    dockerserver.vm.hostname = "dockerserver"
  end
end
