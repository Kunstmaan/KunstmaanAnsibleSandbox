# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"
VAGRANT_HOST_IP = "192.0.0.112"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.define :node do |config|

    config.vm.box = "ubuntu/trusty64"
    config.vm.network "forwarded_port", guest: 80, host: 8888
    config.vm.network "private_network", ip: VAGRANT_HOST_IP
    #config.vm.synced_folder "./", "/var/www/", type: "nfs",  mount_options: ['rw', 'vers=3', 'tcp']
    config.ssh.forward_agent = true
    config.vm.hostname = "node.sandbox"

    config.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--memory", 1024]
      v.customize ["modifyvm", :id, "--ioapic", "on"]
      v.customize ["modifyvm", :id, "--cpus", "1"]
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    end

    if Vagrant.has_plugin?("vagrant-cachier")
      config.cache.scope = :box
    end

    config.vm.provision :ansible do |ansible|
      ansible.playbook = "kunstmaan-setup.yml"
      ansible.inventory_path = "hosts"
      ansible.limit = 'sandboxes'
    end

    config.vm.provision :ansible do |ansible|
      ansible.playbook = "kunstmaan-deploy.yml"
      ansible.inventory_path = "hosts"
      ansible.limit = 'sandboxes'
    end

  end
end
