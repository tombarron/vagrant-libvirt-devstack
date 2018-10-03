# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_DEFAULT_PROVIDER'] = 'libvirt'

Vagrant.configure("2") do |config|

  config.vm.define "devstack-1" do |node|
    node.vm.hostname = "devstack-1"
    node.vm.box = "centos/7"
    node.vm.box_check_update = false
    node.vm.network "private_network", ip: "192.168.18.15"
    node.vm.provider :libvirt do |domain|
      domain.memory = 12288
      domain.cpus = 4
      domain.nested = true
    end
    node.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible-provisioner.yml"
      ansible.verbose = 'v'
    end
  end
end
