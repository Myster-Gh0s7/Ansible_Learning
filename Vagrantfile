# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
 
  config.vm.box = "centos/7"


#config.vm.network "public_network"

  config.vm.define :slave do |slave_config|
    slave_config.vm.hostname = "slave"
    slave_config.vm.network "private_network", ip: "192.168.33.10"
  end
  #Copy cp ~/.ssh/id_rsa . && cp ~/.ssh/id_rsa.pub .
    public_key = File.read("id_rsa.pub")
    config.vm.provision "shell", inline: <<-SCRIPT
        chmod 600 /home/vagrant/.ssh/id_rsa
        echo 'Copying ansible-vm public SSH Keys to the VM'
        #mkdir -p /home/vagrant/.ssh
        chmod 700 /home/vagrant/.ssh
        echo '#{public_key}' >> /home/vagrant/.ssh/authorized_keys
        chmod -R 600 /home/vagrant/.ssh/authorized_keys
        echo 'Host 192.168.*.*' >> /home/vagrant/.ssh/config
        echo 'StrictHostKeyChecking no' >> /home/vagrant/.ssh/config
        echo 'UserKnownHostsFile /dev/null' >> /home/vagrant/.ssh/config
        chmod -R 600 /home/vagrant/.ssh/config
        SCRIPT
    
  
end
