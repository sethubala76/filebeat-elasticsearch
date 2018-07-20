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
	  config.vm.provision "file", source: "docker-compose.yml", destination: "/home/vagrant/docker-compose.yml"
	  config.vm.provision "file", source: "example", destination: "/home/vagrant/example"	  
	  config.vm.provision "file", source: "filebeat", destination: "/home/vagrant/filebeat"		  
	  config.vm.provision "shell", inline: <<-SHELL
		sudo yum check-update
		sudo yum install vim
		curl -fsSL https://get.docker.com/ | sh
		sudo usermod -aG docker vagrant
		sudo systemctl start docker
		sudo systemctl status docker
		sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
		sudo chmod +x /usr/local/bin/docker-compose
		ls -l /var/run/docker.sock
		sudo chmod 666 /var/run/docker.sock
		chmod 755 /usr/local/bin/docker-compose
		sudo sysctl -w vm.max_map_count=262144
		/usr/local/bin/docker-compose -f /home/vagrant/docker-compose.yml -f /home/vagrant/example/httpd.yml up --build -d
	  SHELL
  end
  
