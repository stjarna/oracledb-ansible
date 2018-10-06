Vagrant.configure(2) do |config|

  config.vm.box = "centos/7"
  config.vm.network "private_network", ip: "192.168.56.13"
  config.vm.hostname = "oradb3.private"
  
  config.vm.provider "virtualbox" do |vb|  
    vb.memory = "2048"
    vb.cpus = 2
    vb.name = "Oracle12c-3"
  end
end
