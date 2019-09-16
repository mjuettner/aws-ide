# -*- mode: ruby -*-
# vi: set ft=ruby :
# Mark Juettner, August 2019

# Install required plugins, from: https://stackoverflow.com/a/28801317
required_plugins = %w(vagrant-vbguest)

plugins_to_install = required_plugins.select { |plugin| not Vagrant.has_plugin? plugin }
if not plugins_to_install.empty?
  puts "Installing plugins: #{plugins_to_install.join(' ')}"
  if system "vagrant plugin install #{plugins_to_install.join(' ')}"
    exec "vagrant #{ARGV.join(' ')}"
  else
    abort "Installation of one or more plugins has failed. Aborting."
  end
end

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = true
    vb.memory = "4096"
    vb.cpus = "2"

    # Enable clipboard sharing and drag and drop functionality with the host
    vb.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
    vb.customize ["modifyvm", :id, "--draganddrop", "bidirectional"]
  end

  # Visual Studio Code Extenstions installed via sudo because they install locally to the user
  config.vm.provision "apps", type: "shell", inline: <<-APPS
    apt-get update
    apt-get install -y python3-pip ubuntu-desktop ssh-askpass ruby ntp
    systemctl enable ntp
    gem install cfn-nag
    pip3 install --upgrade boto3 awscli ec2instanceconnectcli cfn-lint
    curl "https://s3.amazonaws.com/session-manager-downloads/plugin/latest/ubuntu_64bit/session-manager-plugin.deb" -o "session-manager-plugin.deb"
    sudo dpkg -i session-manager-plugin.deb
    snap install --classic code
    sudo -H -u vagrant bash -c 'code --install-extension ms-python.python'
    sudo -H -u vagrant bash -c 'code --install-extension ms-vsts.team'
    sudo -H -u vagrant bash -c 'code --install-extension kddejong.vscode-cfn-lint'
    sudo -H -u vagrant bash -c 'code --install-extension eastman.vscode-cfn-nag'
    sudo -H -u vagrant bash -c 'code --install-extension eamodio.gitlens'
    sudo -H -u vagrant bash -c 'code --install-extension dsteenman.cloudformation-yaml-snippets'
    reboot
  APPS
end
