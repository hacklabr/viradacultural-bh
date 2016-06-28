# -*- mode: ruby -*-
# vi: set ft=ruby :

TIMTEC_USER = "vagrant"

$install_dependencies = <<SCRIPT

    sudo apt-get update
    # Install docker
    sudo apt-get install apt-transport-https ca-certificates
    sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
    echo "deb https://apt.dockerproject.org/repo ubuntu-trusty main" | sudo tee /etc/apt/sources.list.d/docker.list
    sudo apt-get install linux-image-extra-$(uname -r)
    sudo apt-get install docker-engine
    # sudo service docker start

    sudo apt-get instal python-pip
    sudo pip install docker-compose

SCRIPT

$runserver = <<SCRIPT
    cd /vagrant
    sudo docker-compose up &

SCRIPT

Vagrant.configure('2') do |config|
  config.vm.box = "ubuntu/trusty64"
  # config.vm.provision :shell, path: "scripts/bootstrap-ubuntu.sh", privileged: false, keep_color: true
  config.vm.provision "shell",
            inline: $runserver,
            privileged: false,
            run: "always"
  config.vm.provision "shell",
            inline: $install_dependencies,
            privileged: false

  config.vm.network "forwarded_port", guest: 80, host: 8080
end
