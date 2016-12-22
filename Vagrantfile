# -*- mode: ruby -*-
# vi: set ft=ruby :

_pwd = Dir.pwd

Vagrant.configure('2') do |config|
  config.vm.define 'debian-dev' do |machine|
    machine.vm.box = "debian/jessie64"
    machine.vm.network :private_network, ip: '10.11.12.13'
    machine.vm.hostname = 'debian-dev'
    machine.vm.provision 'ansible' do |ansible|
      ansible.playbook = 'deb_builder.yml'
      ansible.sudo = true
      ansible.inventory_path = 'vagrant-inventory'
      ansible.host_key_checking = false
    end
    machine.vm.synced_folder _pwd + "/debs", "/usr/local/src"
  end
end
