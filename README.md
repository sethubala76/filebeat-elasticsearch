# filebeat-elasticsearch

sudo yum check-update
curl -fsSL https://get.docker.com/ | sh
sudo usermod -aG docker vagrant
sudo systemctl start docker
sudo systemctl status docker
sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

ls -l /var/run/docker.sock
sudo chmod 666 /var/run/docker.sock
sudo sysctl -w vm.max_map_count=262144


docker-compose -f docker-compose.yml -f example/httpd.yml up

docker-compose -f docker-compose.yml -f example/httpd.yml down
