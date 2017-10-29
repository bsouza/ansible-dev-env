# -*- mode: ruby -*-
# vi: set ft=ruby :

require('./config/config.rb')

BOX_PATH = OPTIONS[:box_path]
BOX_NAME = OPTIONS[:box_name]
USE_CUSTOM_KEY = OPTIONS[:use_custom_key]
CUSTOM_IP = OPTIONS[:custom_ip]

VAGRANT_VERSION = "2"

Vagrant.configure(VAGRANT_VERSION) do |config|

  config.vm.define :ubuntu_dev do |ubuntu_dev|
    ubuntu_dev.vm.box = BOX_PATH
    ubuntu_dev.vm.hostname = BOX_NAME

    if USE_CUSTOM_KEY
      ubuntu_dev.vm.provision "file", source: "keys/public", destination: "~/.ssh/authorized_keys"
      ubuntu_dev.ssh.insert_key = false
      ubuntu_dev.ssh.private_key_path = ["keys/private", "~/.vagrant.d/insecure_private_key"]
    end

    config.vm.network "public_network", ip: CUSTOM_IP

    ubuntu_dev.vm.provider :virtualbox do |virtualbox|
      virtualbox.name = BOX_NAME
      virtualbox.memory = 6144
      virtualbox.cpus = 4
      virtualbox.gui = true
    end

    ubuntu_dev.vm.provision :ansible do |ansible|
      ansible.playbook = "playbook.yml"
    end  
  end

end
