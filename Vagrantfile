# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|

  config.vm.box = "debian/stretch64"
  config.ssh.forward_agent = true
  config.vm.network :public_network
  config.vm.synced_folder ".", "/vagrant", type: "virtualbox"
  config.vbguest.auto_update = true

  config.vm.define "tomcio" do |tomcio|
    tomcio.vm.hostname = "myserver1"
    tomcio.vm.network :private_network, ip: "33.33.33.31"
    tomcio.vm.network "forwarded_port", guest: 8080, host: 8080
    tomcio.vm.network "forwarded_port", guest: 443, host: 443
  end


  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "provisioning/starter.yml"
    ansible.groups = {
      "master" => ["tomcio"]
    }
  end

end