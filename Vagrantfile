# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "debian/bookworm64"
  config.vm.box_check_update = false

  config.vm.provision "shell", inline: <<-SHELL
  apt update
  apt upgrade -y
  SHELL

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 1024
    vb.cpus = 2
  end


  config.vm.define "dhcp" do |dhcp|
    dhcp.vm.network "private_network", ip: "192.168.57.10", virtualbox__intnet: true
    dhcp.vm.network "private_network", ip: "192.168.56.10"

    dhcp.vm.provision "shell", inline: <<-SHELL
    apt-get install -y isc-dhcp-server
    SHELL
  end # dhcp

  config.vm.define "c1" do |client|
   client.vm.network "private_network", type:"dhcp", mac:"B86D5692568E", virtualbox__intnet: true
  end # client

  config.vm.define "c2" do |client|
  client.vm.network "private_network", type:"dhcp", virtualbox__intnet: true
  end # client
  
end














