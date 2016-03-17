# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|

  config.vm.provider "libvirt" do |libvirt, override|
    libvirt.driver = "kvm"
    libvirt.memory = 2048
    libvirt.cpus = 2
  end

  config.vm.define "centos1" do |centos1|
    centos1.vm.box = "centos/7"
    config.vm.hostname = "centos1"
    config.vm.network "private_network", ip: "192.168.50.4"
  end

  config.vm.define "centos2" do |centos2|
    centos2.vm.box = "centos/7"
    config.vm.hostname = "centos2"
    config.vm.network "private_network", ip: "192.168.50.5"
  end

  config.vm.provision "shell", inline: <<-SHELL
     echo '192.168.50.4 centos1' | sudo tee -a /etc/hosts
     echo '192.168.50.5 centos2' | sudo tee -a /etc/hosts

     sudo yum -y update
     sudo yum -y install docker
     sudo systemctl start docker && sudo systemctl enable docker
     sudo curl -L git.io/weave -o /bin/weave
     sudo chmod a+x /bin/weave
     sudo docker pull busybox 
  SHELL

end
