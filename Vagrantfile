# -*- mode: ruby -*-
# vi: set ft=ruby :

box = 'utopic64'
url = 'https://cloud-images.ubuntu.com/vagrant/utopic/current/utopic-server-cloudimg-amd64-vagrant-disk1.box'
ram = '4096'

Vagrant.configure("2") do |config|

  config.vm.box = box
  config.vm.box_url = url
  config.vm.hostname = "localhost"
  config.vm.network "private_network", ip: "192.168.56.102"


  # Provider-specific configuration so you can fine-tune various backing
  # providers for Vagrant. These expose provider-specific options.
  config.vm.provider :virtualbox do |vb|
    # Use VBoxManage to customize the VM
    vb.customize ["modifyvm", :id,
                  "--name", "wildfly",
                  "--memory", ram]
  end

  config.vm.provision :shell, :inline => "echo \"America/Denver\" | sudo tee /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata"

  config.vm.provision :puppet do |puppet|
	puppet.manifests_path = "manifests"
	puppet.manifest_file = "default.pp"
	puppet.module_path = "manifests/modules"
	puppet.options = "--verbose"
  end 

end
