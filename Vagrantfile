
Vagrant.configure("2") do |config|

  ###
  # vagrant box add ubuntu/trusty64
  config.vm.box = "ubuntu/trusty64"

  config.vm.network :private_network, ip: "192.168.50.52"
  config.ssh.forward_agent = true
  config.vm.hostname = "vmname"
  #config.vm.network :forwarded_port, host: 8080, guest: 80

  config.vm.provider :virtualbox do |v|
    v.customize ["modifyvm", :id, "--name", "vmname"]
    v.customize ["modifyvm", :id, "--memory", 1024]
    v.customize ["modifyvm", :id, "--cpus", 2]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end
  
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/bootstrap.yml"
    ansible.verbose = "v"
    ansible.extra_vars = {
      hostname: config.vm.hostname
    }
  end

end
