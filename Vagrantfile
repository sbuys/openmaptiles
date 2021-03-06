# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  #config.vm.box = "ubuntu/trusty64"
  # config.vm.box = "chef/ubuntu-14.04"
  config.vm.box = "bento/ubuntu-16.04"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  config.vm.network "forwarded_port", guest: 80, host: 8080

  # Express server
  # config.vm.network "forwarded_port", guest: 4321, host: 4321

  # Webpack dev server
  # config.vm.network "forwarded_port", guest: 4321, host: 4321

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
   config.vm.network "private_network", ip: "10.0.0.10"
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network", ip: "10.0.0.10"

  #  If true, then any SSH connections made will enable agent forwarding.
  # Default value: false
  config.ssh.forward_agent = true

  #https://github.com/mitchellh/vagrant/issues/5205
  config.ssh.insert_key = false

  #Default is 22?
  #http://docs.vagrantup.com/v2/vagrantfile/ssh_settings.html

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # https://github.com/mitchellh/vagrant/issues/4362
  # config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.synced_folder ".", "/shared", disabled: false

  #config.vm.synced_folder "./app", "/app", :mount_options => ["dmode=777","fmode=766"], type: "rsync", rsync__auto: true, rsync__exclude: [".git/", "node_modules/", "build/", "media/"], rsync__args: ["--verbose", "--archive", "--delete", "-z"]

  # Configure the window for gatling to coalesce writes.
  #if Vagrant.has_plugin?("vagrant-gatling-rsync")
  #  config.gatling.latency = 1
  #  config.gatling.time_format = "%H:%M:%S"
  #end

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Allocate additional memory for virtual machine
  # http://docs.vagrantup.com/v2/virtualbox/configuration.html
  config.vm.provider "vmware_fusion" do |v|
    v.memory = 4096
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/provision.yml"
    ansible.inventory_path = "provisioning/hosts/dev_hosts.yml"
    ansible.sudo = true
    ansible.verbose = "vvvv"
    #limit provisioning to local machine
    ansible.limit = "local"
  end

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   sudo apt-get update
  #   sudo apt-get install -y apache2
  # SHELL
end
