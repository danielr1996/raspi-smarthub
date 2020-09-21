Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  # Copy your own ssh keys for use with ansible
  config.vm.provision "file", source: "~/.ssh/id_ed25519", destination: "/home/vagrant/.ssh/id_ed25519"
  config.vm.provision "file", source: "~/.ssh/id_ed25519.pub", destination: "/home/vagrant/.ssh/id_ed25519.pub"
  config.vm.provision "shell", inline: "chmod 600 /home/vagrant/.ssh/id_ed25519"

  # Export path for pip binaries
  config.vm.provision "shell",inline: "echo 'export PATH=$PATH:/home/vagrant/.local/bin' >> /home/vagrant/.profile"

  # Set /vagrant as default working directory
  config.vm.provision "shell",inline: " echo 'cd /vagrant' >> ~/.bashrc"

  #Install ansible
  config.vm.provision "shell", inline: <<-SHELL
    apt -y update
    apt -y install python3 python3-pip
    su -c "pip3 install ansible" vagrant
  SHELL
end
