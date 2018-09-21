# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define "server", primary: true do |server|
    server.vm.box = "ubuntu/trusty64"
    server.vm.network "private_network", ip: "172.16.0.10", virtualbox__intnet: true
    server.vm.hostname = "server"
    server.vm.provider "virtualbox" do |vb|
      vb.name = "Server"
    end
  end

  config.vm.define "router" do |router|
    router.vm.box = "cisco/csr1000v"
    router.vm.network "private_network", ip: "172.16.0.20", virtualbox__intnet: true, auto_config: false
    router.vm.synced_folder ".", "/vagrant", disabled: true
    router.vm.graceful_halt_timeout = 1
    router.ssh.insert_key = false
    router.vm.provider "virtualbox" do |vb|
      vb.name = "Router"
    end
  end

  config.vm.define "firewall" do |firewall|
    firewall.vm.box = "juniper/ffp-12.1X47-D15.4"
    firewall.vm.network "private_network", ip: "172.16.0.30", virtualbox__intnet: true
    firewall.vm.hostname = "firewall"
    firewall.vm.provider "virtualbox" do |vb|
      vb.name = "Firewall"
      vb.customize ["modifyvm", :id, "--nicpromisc2", "deny"]
    end
  end

  config.vm.box_check_update = false

end
