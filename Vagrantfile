# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_NO_PARALLEL'] = 'yes'

Vagrant.configure(2) do |config|

  config.vm.provision "shell", path: "bootstrap.sh"

  # Kubernetes Master Server
  config.vm.define "kmanager" do |kmanager|
    kmanager.vm.box = "mrlesmithjr/centos7"
    kmanager.vm.hostname = "kmanager.k8.com"
    kmanager.vm.network "private_network", ip: "172.168.33.100"
    kmanager.vm.provider "virtualbox" do |v|
      v.name = "kmanager"
      v.memory = 2048
      v.cpus = 2
    end
    kmanager.vm.provision "shell", path: "bootstrap_kmanager.sh"
  end

  NodeCount = 2

  # Kubernetes Worker Nodes
  (1..NodeCount).each do |i|
    config.vm.define "kworker#{i}" do |workernode|
      workernode.vm.box = "mrlesmithjr/centos7"
      workernode.vm.hostname = "kworker#{i}.k8.com"
      workernode.vm.network "private_network", ip: "172.168.33.10#{i}"
      workernode.vm.provider "virtualbox" do |v|
        v.name = "kworker#{i}"
        v.memory = 1024
        v.cpus = 1
      end
      workernode.vm.provision "shell", path: "bootstrap_kworker.sh"
    end
  end

end
