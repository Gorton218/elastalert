# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"

  config.vm.box_check_update = false
  config.vbguest.auto_update = false

  config.vm.synced_folder ".", "/vagrant"
  config.vm.provider :virtualbox do |p|
    p.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    p.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    p.memory = "512"
  end

  config.vm.provision "shell", inline: <<-SHELL
    PROJECT_NAME=elastalert
    apt-get update
    apt-get install -y python-pip python3-pip
    pip install virtualenv
    for i in $(ls /vagrant/requirements*.txt); do
      pip install -r $i
    done
  SHELL
end
