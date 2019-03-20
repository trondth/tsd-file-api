# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  # More boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "puppetlabs/centos-7.0-64-puppet"


  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Build the rpm
  # rpm -Uvh <name>.rpm to install
  # rom -e <name> to remove
  config.vm.provision "shell", inline: <<-SHELL
    sudo yum -y install emacs rpm-build git
    sudo yum -y install python-devel openssl openssl-devel postgresql-devel
    sudo easy_install pip
    sudo pip install virtualenv virtualenv-tools
    sudo yum -y install ruby-devel gcc make rpm-build rubygems
    sudo gem install --no-ri --no-rdoc fpm
    sudo rm /vagrant/tsd-file-api-venv-1.0-1.x86_64.rpm
    sudo rm /vagrant/python-tsd-file-api-*
    sudo fpm --verbose -v 1.3 -s virtualenv -p /vagrant -t rpm --name tsd-file-api-venv --prefix /opt/tsd-file-api-venv/virtualenv /vagrant/requirements.txt
    sudo fpm -s python -p /vagrant -t rpm /vagrant/setup.py
  SHELL

end
