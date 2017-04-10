# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
	config.vm.box = "centos/7"
	
	config.vm.provider :libvirt do |libvirt|
		libvirt.driver = "kvm"
		libvirt.connect_via_ssh = false
		libvirt.username = "root"
		libvirt.storage_pool_name = "default"
		libvirt.memory = 6000
		libvirt.cpus = 4
	end

	#Application server 1.
	config.vm.define "app1" do |app|
		app.vm.hostname = "app1.dev"
		app.vm.box = "centos/7"
		app.vm.network :private_network, :ip => "192.168.122.4", :mac => "52:54:00:ae:2f:6e"
		app.vm.network "forwarded_port", host: 8080, guest: 80, auto_correct: true
		app.vm.network "forwarded_port", host: 8081, guest: 8080, auto_correct: true
	end

	#Application server 2.
        config.vm.define "app2" do |kas|
                kas.vm.hostname = "app2.dev"
                kas.vm.box = "centos/7"
                kas.vm.network :private_network, :ip => "192.168.122.5", :mac => "52:54:00:ae:2d:7e"
      		kas.vm.network "forwarded_port", host: 8082, guest: 80, auto_correct: true
		kas.vm.network "forwarded_port", host: 8083, guest: 8080, auto_correct: true
	 end


	#DB server 3.
        config.vm.define "db" do |teste|
                teste.vm.hostname = "db.dev"
                teste.vm.box = "centos/7"
                teste.vm.network :private_network, :ip => "192.168.122.6", :mac => "52:54:00:ae:3f:8e"
       		teste.vm.network "forwarded_port", host: 8084, guest: 80, auto_correct: true
		teste.vm.network "forwarded_port", host: 8085, guest: 8080, auto_correct: true
	end

	#config.vm.provision "ansible" do |ansible|
	#       	ansible.playbook = "ntp.yml"
 	#end

	#config.vm.provision "ansible" do |jenkins|
	#	jenkins.playbook = "provision/install.yml"
	#end
	
	#config.vm.provision "ansible" do |appnode|
	#		appnode.playbook = "node.js/install-nodejs.yml"
	#end

	#config.vm.provision "ansible" do |apache|
	#		apache.playbook = "httpd/install-apache.yml"
	#end

	#config.vm.provision "ansible" do |nginx|
	#		nginx.playbook = "nginx/install-nginx.yml"
	#end

	config.vm.provision "ansible" do |ansible|
		ansible.playbook = "provision/install.yml"
		ansible.host_key_checking = false
		ansible.sudo = true
		ansible.tags = ['jenkins']
	end
end
