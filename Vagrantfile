# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.network :forwarded_port, guest: 5000, host: 5000

  config.vm.provision "shell", inline: <<-SHELL
    apt-get install software-properties-common
    add-apt-repository ppa:ondrej/php
    apt-get update

    DEBIAN_FRONTEND=noninteractive apt-get -y install php php-fpm php-gd \
      php-mbstring php-curl php-xml php-mysql zip git npm nginx mysql-server
    
    ln -s /usr/sbin/php-fpm7.0 /usr/sbin/php-fpm
    curl -sS https://getcomposer.org/installer | php
    mv composer.phar /usr/local/bin/composer

    cp /vagrant/nginx.conf /etc/nginx/nginx.conf 
    chmod 777 -R /var/log/nginx/
    
    gem install foreman
  SHELL
end
