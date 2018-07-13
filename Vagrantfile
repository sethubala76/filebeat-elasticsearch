BOX_IMAGE = "geerlingguy/centos7"
NODE_COUNT = 1

Vagrant.configure("2") do |config|

  (1..NODE_COUNT).each do |i|
    config.vm.define "node#{i}" do |subconfig|
      subconfig.vm.box = BOX_IMAGE
      subconfig.vm.hostname = "master#{i}.example.com"
      subconfig.vm.network :private_network, ip: "192.168.33.15"
	  subconfig.vm.network :forwarded_port, guest: 5601, host: 5601
      subconfig.vm.provider "virtualbox" do |v|
        v.memory = 2048
		v.cpus = 2
		end
		  subconfig.ssh.forward_agent = true
		end
	  end
  end
