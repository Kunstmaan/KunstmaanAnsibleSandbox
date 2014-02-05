# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "saucy64"
  config.vm.box_url = 'https://cloud-images.ubuntu.com/vagrant/saucy/current/saucy-server-cloudimg-amd64-vagrant-disk1.box'
  config.vm.network "forwarded_port", guest: 80, host: 8888
  config.vm.network "private_network", ip: "192.168.100.10"

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "kunstmaan/bundles-standard-edition.yml"
    ansible.inventory_path = "kunstmaan/hosts"
  end

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end

end