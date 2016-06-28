# -*- mode: ruby -*-
# vi: set ft=ruby :

$install_dependencies = <<SCRIPT
    sudo sed -i -e 's~http://archive.ubuntu.com/~http://ubuntu.c3sl.ufpr.br/~g' /etc/apt/sources.list
    echo "deb https://apt.dockerproject.org/repo ubuntu-trusty main" | sudo tee /etc/apt/sources.list.d/docker.list
    sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D

    sudo apt-get update
    sudo apt-get install -y docker-engine
    sudo apt-get install -y python-pip
    sudo pip install docker-compose

    sudo adduser vagrant docker
    sudo service docker restart
SCRIPT

$runserver = <<SCRIPT
    sudo -u vagrant -g docker docker-compose -f /vagrant/docker-compose.yml up
SCRIPT

Vagrant.configure('2') do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network "forwarded_port", guest: 80, host: 8080

  config.vm.provision "shell",
            inline: $install_dependencies,
            privileged: false

  config.vm.provision "shell",
            inline: $runserver,
            privileged: true,
            run: "always"
end
