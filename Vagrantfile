# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<-SCRIPT
echo "I like Vagrant"
echo "I love linux"
date > /home/vagrant_provisioned_at
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  config.vm.provision :docker
  config.vm.provision :shell, path: "bootstrap.sh"
  config.vm.provision :file, source: "file.txt", destination: "file.txt"
  config.vm.provision :file, source: "dir1", destination: "dir1"
  config.vm.define "server-1" do |dockerserver|
    dockerserver.vm.network "private_network", ip: '192.168.33.60'
    dockerserver.vm.hostname = "dockerserver"
    dockerserver.vm.provision "shell", inline: "echo Hello world from inline"
    dockerserver.vm.provision "shell", inline: $script
    dockerserver.vm.provision "shell" do |s|
      s.inline = "echo $1 $2"
      s.args = ["AT", "Class!"]
    end
    dockerserver.vm.provision "docker" do |d|
      d.run "hello-world"
    end
  end
end
