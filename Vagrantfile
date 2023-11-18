# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config| 
  config.vm.define "wordpress" do |wordpress|
    wordpress.vm.box = 'centos/7'

    
    wordpress.vm.host_name = 'wordpress'
    wordpress.vm.network "private_network", ip: "192.168.56.10"
    wordpress.vm.network "forwarded_port", guest: 80, host: 8081
    wordpress.vm.network "forwarded_port", guest: 9100, host: 9101
    wordpress.vm.network "forwarded_port", guest: 9080, host: 9081
      
    wordpress.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
    end
    wordpress.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.tags = "wordpress"
    end

  end

  config.vm.define "mysql" do |mysql|
    mysql.vm.box = 'centos/7'

    mysql.vm.host_name = 'mysql'
    mysql.vm.network "private_network", ip: "192.168.56.11"
    mysql.vm.network "forwarded_port", guest: 9100, host: 9100
    mysql.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
    end
    mysql.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.tags = "mysql"
    end
  end    

  config.vm.define "replica" do |replica|
    replica.vm.box = 'centos/7'
    
    replica.vm.host_name = 'replica'
    replica.vm.network "private_network", ip: "192.168.56.12"
      
    replica.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
    end
    replica.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.tags = "replica"
    end
  end

  config.vm.define "monitoring" do |monitoring|
    monitoring.vm.box = 'centos/7'
        
    monitoring.vm.host_name = 'monitoring'
    monitoring.vm.network "private_network", ip: "192.168.56.13"
    monitoring.vm.network "forwarded_port", guest: 3000, host: 3000
    monitoring.vm.network "forwarded_port", guest: 9090, host: 9090
    monitoring.vm.network "forwarded_port", guest: 3100, host: 3100

    monitoring.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
    end
    monitoring.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.tags = "monitoring"
    end
  end
end
