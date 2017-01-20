Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/yakkety64"
  config.vm.network "forwarded_port", guest: 4000, host: 4000
  config.vm.network "private_network", ip: "192.168.3.33",  name: "VirtualBox Host-Only Ethernet Adapter #10"
  config.ssh.forward_agent = true

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", 1024]
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  config.vm.provision "shell", inline: <<-SHELL
    # Update system and install utilities
	sudo apt-get update
	sudo apt-get dist-upgrade
    sudo apt-get install -y git mc

    # Install Jekyll and prerequisites
    sudo apt-get install -y ruby-full ruby-dev zlib1g-dev
    sudo apt-get install -y ruby-dev zlib1g-dev
	gem install bundler
	bundle install --gemfile=/vagrant/Gemfile

	# Install NodeJS
    curl -sL https://deb.nodesource.com/setup_0.12 | sudo bash -
    apt-get install -y nodejs
    sudo npm install -g npm

    # Autostart Jekyll
    jekyll serve --source /vagrant --detach
  SHELL
end
