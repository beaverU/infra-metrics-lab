# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define "metrics-lab" do |node|
    # Using Ubuntu 20.04 LTS (Focal Fossa) as the base box (amd64)
    node.vm.box = "ubuntu/focal64"
    node.vm.hostname = "infra-metrics-lab"

    # Create a forwarded port mapping which allows access to a specific port
    # within the machine from a port on the host machine and only allow access
    # via 127.0.0.1 to disable public access
    node.vm.network "forwarded_port", guest: 3000, host: 3000, host_ip: "127.0.0.1"
    node.vm.network "forwarded_port", guest: 9090, host: 9090, host_ip: "127.0.0.1"

    # Create a private network, which allows host-only access to the machine
    # using a specific IP.
    node.vm.network "private_network", ip: "192.168.36.10"

    # Provider-specific configuration so you can fine-tune various
    # backing providers for Vagrant. These expose provider-specific options.
    # Example for VirtualBox:
    node.vm.provider "virtualbox" do |vb|
      # Customize the amount of memory on the VM:
      vb.memory = "2048"
      vb.cpus = 2
      vb.name = "infra-metrics-lab"
      vb.customize ["modifyvm", :id, "--cpuexecutioncap", "70"]
    end

    # Running ansible_local provisioner in order to avoid external dependencies
    node.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "/vagrant/ansible/playbook.yml"
      #ansible.inventory_path = "/vagrant/ansible/inventory"
      #ansible.verbose = true
      #ansible.limit = "all"
    end
  end
end
