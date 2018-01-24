$workstation_script = <<SCRIPT
wget https://packages.chef.io/files/stable/chefdk/2.4.17/ubuntu/14.04/chefdk_2.4.17-1_amd64.deb
sudo dpkg -i chefdk_2.4.17-1_amd64.deb
mkdir /home/vagrant/learn-chef
sudo apt-get update
sudo apt-get install -y git
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.define "workstation" do |workstation|
     workstation.vm.box = "bento/ubuntu-14.04"
     workstation.vm.hostname = "workstation"
     workstation.vm.network "private_network", type: "dhcp"
     workstation.vm.provision "shell", inline: $workstation_script
  end

  config.vm.define "chefserver" do |chefserver|
     chefserver.vm.box = "bento/ubuntu-14.04"
     chefserver.vm.hostname = "chefserver"
     chefserver.vm.network "private_network", type: "dhcp"
     chefserver.vm.provision "shell", path: "install-chef-server.sh", privileged: true
  end

  config.vm.define "node" do |node|
     node.vm.box = "bento/ubuntu-14.04"
     node.vm.hostname = "node"
     node.vm.network "private_network", type: "dhcp"
  end
end
