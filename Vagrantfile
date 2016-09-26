# -*- mode: ruby -*-
# # vi: set ft=ruby :

Vagrant.require_version '>= 1.6.0'

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure('2') do |config|
    # The most common configuration options are documented and commented below.
    # For a complete reference, please see the online documentation at
    # https://docs.vagrantup.com.

    # Every Vagrant development environment requires a box. You can search for
    # boxes at https://atlas.hashicorp.com/search.

    config.vm.box = 'coreos-stable'
    config.vm.box_url = 'https://storage.googleapis.com/stable.release.core-os.net/amd64-usr/current/coreos_production_vagrant.json'

    config.vm.provider :virtualbox do |v|
        # On VirtualBox, we don't have guest additions or a functional vboxsf
        # in CoreOS, so tell Vagrant that so it can be smarter.
        v.check_guest_additions = false
        v.functional_vboxsf = false
    end

    # plugin conflict
    config.vbguest.auto_update = false if Vagrant.has_plugin?('vagrant-vbguest')

    #  if $enable_serial_logging
    #    logdir = File.join(File.dirname(__FILE__), "log")
    #    FileUtils.mkdir_p(logdir)

    #    serialFile = File.join(logdir, "%s-serial.txt" % vm_name)
    #    FileUtils.touch(serialFile)

    #    config.vm.provider :virtualbox do |vb, override|
    #      vb.customize ["modifyvm", :id, "--uart1", "0x3F8", "4"]
    #      vb.customize ["modifyvm", :id, "--uartmode1", serialFile]
    #    end
    #  end

    # Disable automatic box update checking. If you disable this, then
    # boxes will only be checked for updates when the user runs
    # `vagrant box outdated`. This is not recommended.
    # config.vm.box_check_update = false

    # Create a forwarded port mapping which allows access to a specific port
    # within the machine from a port on the host machine. In the example below,
    # accessing "localhost:8080" will access port 80 on the guest machine.
    # config.vm.network "forwarded_port", guest: 80, host: 8080

    #  if $expose_docker_tcp
    #    config.vm.network "forwarded_port", guest: 2375, host: ($expose_docker_tcp + i - 1), host_ip: "127.0.0.1", auto_correct: true
    #  end

    #  $forwarded_ports.each do |guest, host|
    #    config.vm.network "forwarded_port", guest: guest, host: host, auto_correct: true
    #  end

    config.vm.network 'forwarded_port', guest: 8080, host: 16_981, auto_correct: true

    # Create a private network, which allows host-only access to the machine
    # using a specific IP.
    # config.vm.network "private_network", ip: "192.168.33.10"

    # Create a public network, which generally matched to bridged network.
    # Bridged networks make the machine appear as another physical device on
    # your network.
    # config.vm.network "public_network"

    # Share an additional folder to the guest VM. The first argument is
    # the path on the host to the actual folder. The second argument is
    # the path on the guest to mount the folder. And the optional third
    # argument is a set of non-required options.
    # config.vm.synced_folder "../data", "/vagrant_data"

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

    # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
    # such as FTP and Heroku are also available. See the documentation at
    # https://docs.vagrantup.com/v2/push/atlas.html for more information.
    # config.push.define "atlas" do |push|
    #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
    # end

    # Enable provisioning with a shell script. Additional provisioners such as
    # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
    # documentation for more information about their specific syntax and use.
    config.vm.provision 'shell', inline: <<-SHELL
       docker pull cerestech/jira-coreos
       docker run -d -p 8080:8080 cerestech/jira-coreos
    SHELL
end
