# -*- mode: ruby -*- 
# vi: set ft=ruby : 
# Every Vagrant development environment requires a box. You can search for 
# boxes at https://atlas.hashicorp.com/search.
BOX_IMAGE = "centos/7" 
NODE_COUNT = 2 
Vagrant.configure("2") do |config|  

  config.vm.define "nfs" do |subconfig|  
    subconfig.vm.box = BOX_IMAGE   
    subconfig.vm.hostname = "nfs"   
    subconfig.vm.network :private_network, ip: "10.0.0.9"  
    subconfig.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "2048"]
    end
  end
  config.vm.define "master" do |subconfig|  
      subconfig.vm.box = BOX_IMAGE   
      subconfig.vm.hostname = "master"   
      subconfig.vm.network :private_network, ip: "10.0.0.10"  
      subconfig.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "2048"]
      end
  end     
  (1..NODE_COUNT).each do |i|   
     config.vm.define "node#{i}" do |subconfig|  
          subconfig.vm.box = BOX_IMAGE      
          subconfig.vm.hostname = "node#{i}"   
          subconfig.vm.network :private_network, ip: "10.0.0.#{i + 10}" 
          subconfig.vm.provider :virtualbox do |vb|
            vb.customize ["modifyvm", :id, "--memory", "2048"]
          end
     end   
   end   
   # Install avahi on all machines 
   config.vm.provision "shell",
    inline: "sudo yum install -y avahi-tools avahi-ui-tools"    
end