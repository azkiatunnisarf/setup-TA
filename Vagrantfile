# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
 
    config.vm.box = "azkiafajriyati/myits20"
    config.vm.network "forwarded_port", guest: 80, host: 9000, host_ip: "127.0.0.1"
    config.vm.provision "shell", path: "setup.sh"
    config.vm.provision "init", type: "ansible" do |ansible|
      ansible.playbook = "initial-setup.yml"
    end
    config.vm.provision "req", type: "ansible" do |ansible|
      ansible.galaxy_role_file = 'requirements.yml'
      ansible.galaxy_roles_path = '/etc/ansible/roles'
      ansible.galaxy_command = 'ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path}'
      ansible.playbook = "setup.yml"
    end
    config.vm.provision "setup", type: "ansible" do |ansible|
      
      ansible.playbook = "setup.yml"
      ansible.tags = "user,nginx"
  
    end
    config.vm.provision "deploy", type: "ansible" do |ansible|
      ansible.playbook = "deploy.yml"
  
    end
    
    config.vm.provision "perm", type: :shell, inline: <<~'EOM'
      sudo chmod 777 ~/.ansible/galaxy_token
    EOM
   
  end
  