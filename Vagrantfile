# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", 2048]
    v.customize ["modifyvm", :id, "--cpus", 4]
  end

  config.vm.network :forwarded_port, guest: 5000, host: 5000

  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    # Update and install common dependencies
    export DEBIAN_FRONTEND=noninteractive
    sudo apt-get update
    sudo apt-get -y install libmcrypt-dev libreadline-dev git
    sudo -E apt-get -y build-dep php5-cli

    # Install php-build and compile PHP 7.0.4
    git clone git://github.com/php-build/php-build
    cd php-build
    sudo ./install.sh
    php-build 7.0.4 /home/vagrant/.phps/7.0.4/
    cd

    # Install php-version and set default version
    git clone https://github.com/wilmoore/php-version.git
    source $HOME/php-version/php-version.sh && php-version 7.0.4    
    echo 'source $HOME/php-version/php-version.sh && php-version 7.0.4' >> ~/.bashrc

    # Install Composer
    curl -sS https://getcomposer.org/installer | php
    sudo mv composer.phar /usr/local/bin/composer

    # Install nginx
    sudo apt-get -y install nginx
    sudo cp /vagrant/nginx.conf /etc/nginx/nginx.conf 
    sudo chmod 777 -R /var/log/nginx/

    # Install foreman    
    sudo gem install foreman
  SHELL
end
