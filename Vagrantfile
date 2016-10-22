# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.box_check_update = false
    # To create and import virtualbox box you need to run those commands:
    # git clone https://github.com/oisis/packer-centos7
    # cd ./packer-centos7
    # packer build -only=virtualbox-iso template.json
    # vagrant box add centos71 ./centos71-x64-virtualbox.box
    # If you already have box centos71 and would like to switch
    # to new one run this command: vagrant box remove centos71
    config.vm.box = "centos71"
    config.vm.provider :virtualbox do |vb|
        vb.gui = false
    end

$fill_hosts = <<SCRIPT
cat > /etc/hosts <<EOF
127.0.0.1 localhost localhost.localdomain localhost4 localhost4.localdomain4
::1       localhost localhost.localdomain localhost6 localhost6.localdomain6
192.168.0.2 etcd1.vagrant.loc etcd1
192.168.0.3 etcd2.vagrant.loc etcd2
192.168.0.4 etcd3.vagrant.loc etcd3
192.168.0.10 k8s1.vagrant.loc k8s1
192.168.0.11 k8s2.vagrant.loc k8s2
192.168.0.20 node1.vagrant.loc node1
192.168.0.21 node2.vagrant.loc node2
192.168.0.100 lb.vagrant.loc lb
192.168.0.240 test.vagrant.loc test
EOF
SCRIPT

  config.vm.define "etcd1" do |config|
    config.vm.hostname = "etcd1.vagrant.loc"
    config.vm.provision "shell", inline: $fill_hosts
    config.vm.network :private_network,ip: "192.168.0.2"
    config.vm.provision :ansible do |ansible|
      # ansible.verbose = "vvvv"
      ansible.playbook = "playbook.yaml"
      ansible.inventory_path = "environments/vagrant/inventory"
      ansible.raw_arguments  = [ "--connection=paramiko", "-e env=vagrant" ]
    end
    config.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "256", "--cpus", 1, "--ioapic", "on", "--cpuexecutioncap", "50"]
    end
  end

  config.vm.define "etcd2" do |config|
    config.vm.hostname = "etcd2.vagrant.loc"
    config.vm.provision "shell", inline: $fill_hosts
    config.vm.network :private_network,ip: "192.168.0.3"
    config.vm.provision :ansible do |ansible|
      ansible.verbose = "false"
      ansible.playbook = "playbook.yaml"
      ansible.inventory_path = "environments/vagrant/inventory"
      ansible.raw_arguments  = [ "--connection=paramiko", "-e env=vagrant"]
    end
    config.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "256", "--cpus", 1, "--ioapic", "on", "--cpuexecutioncap", "50"]
    end
  end

  config.vm.define "etcd3" do |config|
    config.vm.hostname = "etcd3.vagrant.loc"
    config.vm.provision "shell", inline: $fill_hosts
    config.vm.network :private_network,ip: "192.168.0.4"
    config.vm.provision :ansible do |ansible|
      ansible.verbose = "false"
      ansible.playbook = "playbook.yaml"
      ansible.inventory_path = "environments/vagrant/inventory"
      ansible.raw_arguments  = [ "--connection=paramiko", "-e env=vagrant"]
    end
    config.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "256", "--cpus", 1, "--ioapic", "on", "--cpuexecutioncap", "50"]
    end
  end


  config.vm.define "k8s1" do |config|
    config.vm.hostname = "k8s1.vagrant.loc"
    config.vm.provision "shell", inline: $fill_hosts
    config.vm.network :private_network,ip: "192.168.0.10"
    config.vm.network :forwarded_port, guest: 8080, host: 8080
    config.vm.provision :ansible do |ansible|
      ansible.verbose = "false"
      ansible.playbook = "playbook.yaml"
      ansible.inventory_path = "environments/vagrant/inventory"
      ansible.raw_arguments  = [ "--connection=paramiko", "-e env=vagrant"]
    end
    config.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "512", "--cpus", 1, "--ioapic", "on", "--cpuexecutioncap", "50"]
    end
  end

  config.vm.define "k8s2" do |config|
    config.vm.hostname = "k8s2.vagrant.loc"
    config.vm.provision "shell", inline: $fill_hosts
    config.vm.network :private_network,ip: "192.168.0.11"
    config.vm.provision :ansible do |ansible|
      ansible.verbose = "false"
      ansible.playbook = "playbook.yaml"
      ansible.inventory_path = "environments/vagrant/inventory"
      ansible.raw_arguments  = [ "--connection=paramiko", "-e env=vagrant"]
    end
    config.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "512", "--cpus", 1, "--ioapic", "on", "--cpuexecutioncap", "50"]
    end
  end

  config.vm.define "node1" do |config|
    config.vm.hostname = "node1.vagrant.loc"
    config.vm.provision "shell", inline: $fill_hosts
    config.vm.network :private_network,ip: "192.168.0.20"
    config.vm.provision :ansible do |ansible|
      ansible.verbose = "false"
      ansible.playbook = "playbook.yaml"
      ansible.inventory_path = "environments/vagrant/inventory"
      ansible.raw_arguments  = [ "--connection=paramiko", "-e env=vagrant"]
    end
    config.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "1024", "--cpus", 1, "--ioapic", "on", "--cpuexecutioncap", "50"]
    end
  end

  config.vm.define "node2" do |config|
    config.vm.hostname = "node2.vagrant.loc"
    config.vm.provision "shell", inline: $fill_hosts
    config.vm.network :private_network,ip: "192.168.0.21"
    config.vm.provision :ansible do |ansible|
      ansible.verbose = "false"
      ansible.playbook = "playbook.yaml"
      ansible.inventory_path = "environments/vagrant/inventory"
      ansible.raw_arguments  = [ "--connection=paramiko", "-e env=vagrant"]
    end
    config.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "1024", "--cpus", 1, "--ioapic", "on", "--cpuexecutioncap", "50"]
    end
  end

  config.vm.define "lb" do |config|
    config.vm.hostname = "lb.vagrant.loc"
    config.vm.provision "shell", inline: $fill_hosts
    config.vm.network :private_network,ip: "192.168.0.100"
    config.vm.network :forwarded_port, guest: 1936, host: 1936
    config.vm.network :forwarded_port, guest: 2379, host: 2379
    config.vm.network :forwarded_port, guest: 4001, host: 4001
    config.vm.provision :ansible do |ansible|
      ansible.verbose = "false"
      ansible.playbook = "playbook.yaml"
      ansible.inventory_path = "environments/vagrant/inventory"
      ansible.raw_arguments  = [ "--connection=paramiko", "-e env=vagrant"]
    end
    config.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "512", "--cpus", 1, "--ioapic", "on", "--cpuexecutioncap", "50"]
    end
  end

  config.vm.define "test" do |config|
    config.vm.hostname = "test.vagrant.loc"
    config.vm.provision "shell", inline: $fill_hosts
    config.vm.network :private_network,ip: "192.168.0.240"
    config.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "1024", "--cpus", 1, "--ioapic", "on", "--cpuexecutioncap", "50"]
    end
  end
end
