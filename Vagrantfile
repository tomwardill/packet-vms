# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define :alpha do |alpha|
    alpha.vm.box = "debian/bookworm64"
    alpha.vm.network "private_network", ip: "192.168.56.2"
    alpha.vm.hostname = "alpha"

    alpha.vm.provider "virtualbox" do |vb|
      vb.name = "ad25dev-alpha"
      vb.gui = true
      vb.memory = "2048"
      vb.cpus = 2
      vb.linked_clone = true
      vb.customize ["modifyvm", :id, "--vram", "128"]
    end

    alpha.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible/playbook.yml"
      ansible.extra_vars = { "callsign" => "alpha", "alpha" => "192.168.56.2", "beta" => "192.168.56.3"}
      ansible.verbose = true
    end

    alpha.vm.provision "reboot", type: "shell", inline: "", reboot: true
  end

  config.vm.define :beta do |beta|
    beta.vm.box = "debian/bookworm64"
    beta.vm.network "private_network", ip: "192.168.56.3"
    beta.vm.hostname = "beta"

    beta.vm.provider "virtualbox" do |vb|
      vb.name = "ad25dev-beta"
      vb.gui = true
      vb.memory = "2048"
      vb.cpus = 2
      vb.linked_clone = true
    end

    beta.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible/playbook.yml"
      ansible.extra_vars = { "callsign" => "beta", "alpha" => "192.168.56.2", "beta" => "192.168.56.3"}
      ansible.verbose = true
    end

    beta.vm.provision "reboot", type: "shell", inline: "", reboot: true
  end

end
