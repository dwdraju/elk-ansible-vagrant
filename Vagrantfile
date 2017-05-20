# -*- mode: ruby -*-
# vi: set ft=ruby :
VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
config.ssh.private_key_path = "~/.vagrant.d/insecure_private_key"
config.ssh.insert_key = false
config.ssh.paranoid = true
	config.vm.box = "geerlingguy/ubuntu1604"
	config.vm.provider :virtualbox do |v|
		v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
		v.customize ["modifyvm", :id, "--memory", 1024]
		v.customize ["modifyvm", :id, "--cpus", 2]
		v.customize ["modifyvm", :id, "--ioapic", "on"]
	end
# ELK server.
	config.vm.define "elk" do |elk|
		elk.vm.hostname = "elk"
		elk.vm.network :private_network, ip: "192.168.9.90"
		elk.vm.provision :ansible do |ansible|
			ansible.playbook = "playbook.yml"
			ansible.inventory_path = "inventory"
			ansible.sudo = true
#			ansible.verbose = "vvv"
			end
		end
	
# Web server.
config.vm.define "webs" do |webs|
webs.vm.hostname = "webs"
webs.vm.network :private_network, ip: "192.168.9.91"
webs.vm.provision :ansible do |ansible|
ansible.playbook = "web/playbook.yml"
ansible.inventory_path = "web/inventory"
ansible.sudo = true
end
end
end