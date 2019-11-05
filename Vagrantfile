# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--audio", "none"]
  end

# Bootstrap for Ansible
  config.vm.provision "shell",
    inline: "DEBIAN_FRONTEND=noninteractive sudo apt-get -y install python"

  config.vm.box      = "ubuntu/bionic64"
  config.vm.hostname = "tester"
  config.vm.network "forwarded_port", guest: 9093, host: 9093
  config.vm.network "forwarded_port", guest: 9090, host: 9090

  config.vm.provision "ansible" do |ansible|
    ansible.playbook           = "tests/test.yml"
    ansible.become             = "true"
    ansible.compatibility_mode = "2.0"
  end


end
