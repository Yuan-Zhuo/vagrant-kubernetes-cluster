# -*- mode: ruby -*-
# vi: set ft=ruby :

MASTER_IP       = "192.168.56.10"
NODE_01_IP      = "192.168.56.11"
NODE_02_IP      = "192.168.56.12"

Vagrant.configure("2") do |config|
  config.vm.box = "geerlingguy/ubuntu2004"
  config.vm.box_version = "1.0.3"

  boxes = [
    { :name => "kube-master",  :ip => MASTER_IP,  :cpus => 2, :memory => 4096 },
    { :name => "kube-node-01", :ip => NODE_01_IP, :cpus => 2, :memory => 4096 },
    { :name => "kube-node-02", :ip => NODE_02_IP, :cpus => 2, :memory => 4096 },
  ]

  boxes.each do |opts|
    config.vm.define opts[:name] do |box|
      box.vm.hostname = opts[:name]
      box.vm.network :private_network, ip: opts[:ip]
 
      box.vm.provider "virtualbox" do |vb|
        vb.cpus = opts[:cpus]
        vb.memory = opts[:memory]
      end
      box.vm.provision "shell", path:"./install-kubernetes-dependencies.sh"
      if box.vm.hostname == "kube-master" then 
        box.vm.provision "shell", path:"./configure-master-node.sh"
      else
        box.vm.provision "shell", path:"./configure-worker-nodes.sh"
      end
    end
  end
end