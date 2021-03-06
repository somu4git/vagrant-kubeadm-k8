Vagrant.configure("2") do |config|
    config.vm.provision "shell", inline: <<-SHELL
        apt-get update -y
        echo "192.168.56.10  master-node" >> /etc/hosts
        echo "192.168.56.11  worker-node01" >> /etc/hosts
        echo "192.168.56.12  worker-node02" >> /etc/hosts
    SHELL
    
    config.vm.define "master" do |master|
      master.vm.box = "bento/ubuntu-18.04"
      config.vm.boot_timeout = 900
      master.vm.hostname = "master-node"
      master.vm.network "private_network", ip: "192.168.56.10"
      master.vm.provider "virtualbox" do |vb|
          vb.memory = 1024
          vb.cpus = 1
      end
      master.vm.provision "shell", path: "scripts/common.sh"
      master.vm.provision "shell", path: "scripts/master.sh"
      master.vm.provision "shell", path: "scripts/update-dns.sh"
    end

    (1..2).each do |i|
  
    config.vm.define "node0#{i}" do |node|
      node.vm.box = "bento/ubuntu-18.04"
      config.vm.boot_timeout = 900
      node.vm.hostname = "worker-node0#{i}"
      node.vm.network "private_network", ip: "192.168.56.1#{i}"
      node.vm.provider "virtualbox" do |vb|
          vb.memory = 512
          vb.cpus = 1
      end
      node.vm.provision "shell", path: "scripts/common.sh"
      node.vm.provision "shell", path: "scripts/node.sh"
      node.vm.provision "shell", path: "scripts/update-dns.sh"
    end
    
    end
  end
