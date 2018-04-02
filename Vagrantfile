# -*- mode: ruby -*-
# vi: set ft=ruby :
# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

Vagrant.configure("2") do |config|

  config.vm.define "webServer" do |webServer|
    webServer.vm.box = "./precise64.box"
    webServer.vm.network "private_network", ip: "192.168.30.11"
	webServer.vm.hostname = "webServer"
	webServer.vm.provider "virtualoadbalanceox" do |vb|
      vb.memory = "512"
	  vb.name = "webServer"
    end
	webServer.vm.provision "shell", inline: <<-SHELL
      sudo echo "192.168.30.10 ansibleControl" >> /etc/hosts
	  sudo echo "192.168.30.11 webServer" >> /etc/hosts
	  sudo echo "192.168.30.12 db" >> /etc/hosts
    SHELL
  end
  
    config.vm.define "webServer01" do |webServer01|
    webServer01.vm.box = "./precise64.box"
    webServer01.vm.network "private_network", ip: "192.168.30.13"
	webServer01.vm.hostname = "webServer01"
	webServer01.vm.provider "virtualoadbalanceox" do |vb|
      vb.memory = "512"
	  vb.name = "webServer01"
    end
	webServer01.vm.provision "shell", inline: <<-SHELL
      sudo echo "192.168.30.10 ansibleControl" >> /etc/hosts
	  sudo echo "192.168.30.11 webServer" >> /etc/hosts
	  sudo echo "192.168.30.12 db" >> /etc/hosts
    SHELL
  end
  
    config.vm.define "loadbalance" do |loadbalance|
    loadbalance.vm.box = "./precise64.box"
    loadbalance.vm.network "private_network", ip: "192.168.30.14"
	loadbalance.vm.hostname = "loadbalance"
	loadbalance.vm.provider "virtualoadbalanceox" do |vb|
      vb.memory = "512"
	  vb.name = "loadbalance"
    end
	loadbalance.vm.provision "shell", inline: <<-SHELL
      sudo echo "192.168.30.10 ansibleControl" >> /etc/hosts
	  sudo echo "192.168.30.11 webServer" >> /etc/hosts
	  sudo echo "192.168.30.12 db" >> /etc/hosts
	  sudo echo "192.168.30.13 webServer01" >> /etc/hosts
    SHELL
  end

  
  config.vm.define "db" do |db|
    db.vm.box = "./precise64.box"
    db.vm.network "private_network", ip: "192.168.30.12"
    db.vm.hostname = "db"
	db.vm.provider "virtualoadbalanceox" do |vb|
      vb.memory = "512"
	  vb.name = "db"
    end
	db.vm.provision "shell", inline: <<-SHELL
      sudo echo "192.168.30.10 ansibleControl" >> /etc/hosts
	  sudo echo "192.168.30.11 webServer" >> /etc/hosts
	  sudo echo "192.168.30.12 db" >> /etc/hosts
    SHELL
  end
  
  config.vm.define "ansibleControl" do |ansibleControl|
    ansibleControl.vm.box = "./precise64.box"
    ansibleControl.vm.network "private_network", ip: "192.168.30.10"
	ansibleControl.vm.hostname ="ansibleControl"
	ansibleControl.vm.provider "virtualoadbalanceox" do |vb|
      vb.memory = "512"
	  vb.name = "ansibleControl"
    end
	
	ansibleControl.vm.provision "shell", inline: <<-SHELLSUDO
      sudo echo "192.168.30.10 ansibleControl" >> /etc/hosts
	  sudo echo "192.168.30.11 webServer" >> /etc/hosts
	  sudo echo "192.168.30.12 db" >> /etc/hosts
	  sudo echo "192.168.30.13 webServer01" >> /etc/hosts
      sudo echo "192.168.30.13 loadbalance" >> /etc/hosts
	  sudo apt-get -y install sshpass
   	  sudo apt-get update
	  sudo apt-get -y install software-properties-common python-software-properties
	  sudo apt-add-repository ppa:ansible/ansible
	  sudo apt-get update
	  sudo apt-get -y install ansible
    SHELLSUDO
	
	ansibleControl.vm.provision "shell", privileged: false, inline: <<-SHELL
	  ssh-keygen -t rsa -P "" -f ~/.ssh/id_rsa
	  echo "StrictHostKeyChecking no" >> ~/.ssh/config
	  sshpass -p "vagrant" ssh-copy-id -i /home/vagrant/.ssh/id_rsa.pub vagrant@webServer
      sshpass -p "vagrant" ssh-copy-id -i /home/vagrant/.ssh/id_rsa.pub vagrant@webServer01
	  sshpass -p "vagrant" ssh-copy-id -i /home/vagrant/.ssh/id_rsa.pub vagrant@db
      sshpass -p "vagrant" ssh-copy-id -i /home/vagrant/.ssh/id_rsa.pub vagrant@loadbalance
    SHELL
		
  end
  
end