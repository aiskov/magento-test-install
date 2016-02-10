Magento Test Install
====================

Example of Vagrantfile:

    Vagrant.configure("2") do |config|
        config.vm.box = "ubuntu/trusty64"
        config.vm.network "public_network", auto_config: true
      
        config.vm.provision "ansible" do |ansible|
            ansible.playbook = "playbooks/init.yml"
        end
      
        config.vm.provision "ansible" do |ansible|
            ansible.verbose = "vv"
            ansible.playbook = "playbooks/magento/install-1.6.yml"
        end
      
        config.vm.provision "shell", run: "always" do |shell|
            shell.inline = "ifconfig"
        end
      
        config.vm.synced_folder "magento/", "/var/www/magento", :mount_options => ['dmode=777', 'fmode=777']
    end

Requirments
-----------

* VM (as example VirtualBox https://www.virtualbox.org/wiki/Downloads)
* Vagrant https://www.vagrantup.com/downloads.html
* Ansible http://docs.ansible.com/ansible/intro_installation.html#installing-the-control-machine
