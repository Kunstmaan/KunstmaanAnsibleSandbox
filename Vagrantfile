Vagrant::Config.run do |config|



  config.vm.define :web do |web_config|
    web_config.vm.box = "saucy64"
    web_config.vm.box_url = 'http://cloud-images.ubuntu.com/vagrant/saucy/current/saucy-server-cloudimg-amd64-vagrant-disk1.box'
    web_config.vm.forward_port 80, 8888
    web_config.vm.forward_port 81, 8889
    web_config.vm.network :bridged
    web_config.vm.network :hostonly, "192.168.100.10"

    web_config.vm.provision :ansible do |ansible|
      ansible.playbook = "kunstmaan/bundles-standard-edition.yml"
      ansible.inventory_path = "kunstmaan/hosts"
    end


  end

  config.vm.customize [
                        "modifyvm", :id,
                        "--memory", "1024"
                      ]

end