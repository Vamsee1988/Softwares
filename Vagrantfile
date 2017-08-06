Vagrant.configure("2") do |config|
  config.vm.define "server1" do |server1|
    server1.vm.box = "bento/centos-7.2"
    server1.vm.network "private_network", ip: "192.168.70.10"
  end

  config.vm.define "chefmachine" do |chefmachine|
    chefmachine.vm.box = "bento/centos-7.2"
    chefmachine.vm.network "private_network", ip: "192.168.70.11"
  end
  
   config.vm.define "centos1" do |centos1|
    centos1.vm.box = "bento/centos-7.2"
    centos1.vm.network "private_network", ip: "192.168.70.12"
  end
  
   config.vm.define "dockernode" do |dockernode|
    dockernode.vm.box = "bento/centos-7.2"
    dockernode.vm.network "private_network", ip: "192.168.70.13"
	dockernode.vm.network "forwarded_port", guest:80, host:9090
  end
  
  config.vm.define "nagiosnode" do |nagiosnode|
    nagiosnode.vm.box = "bento/centos-7.2"
    nagiosnode.vm.network "private_network", ip: "192.168.70.14"
  end
  
 
  
# Defines our Vagrant environment
#
# -*- mode: ruby -*-
# vi: set ft=ruby :


  # create mgmt node
  config.vm.define :mgmt do |mgmt_config|
      mgmt_config.vm.box = "ubuntu/trusty64"
      mgmt_config.vm.hostname = "mgmt"
      mgmt_config.vm.network :private_network, ip: "10.0.15.10"
      mgmt_config.vm.provider "virtualbox" do |vb|
        vb.memory = "256"
      end
    
  end

  # create load balancer
  config.vm.define :lb do |lb_config|
      lb_config.vm.box = "ubuntu/trusty64"
      lb_config.vm.hostname = "lb"
      lb_config.vm.network :private_network, ip: "10.0.15.11"
      lb_config.vm.network "forwarded_port", guest: 80, host: 8080
      lb_config.vm.provider "virtualbox" do |vb|
        vb.memory = "256"
      end
  end
  
 
  # create some web servers
  # https://docs.vagrantup.com/v2/vagrantfile/tips.html
  (1..2).each do |i|
    config.vm.define "web#{i}" do |node|
        node.vm.box = "ubuntu/trusty64"
        node.vm.hostname = "web#{i}"
        node.vm.network :private_network, ip: "10.0.15.2#{i}"
        node.vm.network "forwarded_port", guest: 80, host: "808#{i}"
        node.vm.provider "virtualbox" do |vb|
          vb.memory = "256"
        end
    end
  end
  
  # create centos vm
  config.vm.define :web11 do |web11_config|
      web11_config.vm.box = "bento/centos-7.2"
      web11_config.vm.hostname = "web11"
      web11_config.vm.network :private_network, ip: "10.0.15.75"
      web11_config.vm.network "forwarded_port", guest: 80, host: 1234
      web11_config.vm.provider "virtualbox" do |vb|
        vb.memory = "256"
      end
  end

end