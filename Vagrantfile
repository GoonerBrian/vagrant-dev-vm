# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "ubuntu/jammy64"

  # For GUI (Desktop) mode:
  # config.vm.box = "peru/ubuntu-24.04-desktop-amd64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
  config.vm.network "forwarded_port", guest: 22, host: 2222, id: "ssh"

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

  # Disable the default share of the current code directory. Doing this
  # provides improved isolation between the vagrant box and your host
  # by making sure your Vagrantfile isn't accessible to the vagrant box.
  # If you use this you may want to enable additional shared subfolders as
  # shown above.
  # config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.synced_folder ".", "/vagrant", type: "virtualbox"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    # Uncomment the next line for GUI mode
    # vb.gui = true
  
    # Customize the amount of memory on the VM:
    vb.memory = "16384"

    # Customize the number of CPUs
    vb.cpus = 8

  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL

  # Provision C/C++ tools
  config.vm.provision "shell", inline: <<-SHELL
    # Update system and base packages
    sudo apt update
    sudo apt install -y \
      build-essential \
      gdb \
      cmake \
      clang \
      curl \
      software-properties-common \
      apt-transport-https \
      wget \
      git

    # ---- Python (latest stable from deadsnakes) ----
    sudo add-apt-repository ppa:deadsnakes/ppa -y
    sudo apt update
    sudo apt install -y python3.13 python3.13-venv python3.13-dev python3-pip
    sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.13 1
    sudo update-alternatives --install /usr/bin/pip pip /usr/bin/pip3 1

    # ---- Optional Python dev tools ----
    sudo pip install --upgrade pip setuptools wheel virtualenv black flake8

    # ---- (Optional) VS Code for GUI mode ----
    # Comment this section out if using VS Code Remote SSH only
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
    sudo install -o root -g root -m 644 packages.microsoft.gpg /usr/share/keyrings/
    sudo sh -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/packages.microsoft.gpg] \
      https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'
    sudo apt update
    sudo apt install -y code
    rm packages.microsoft.gpg

    # ---- VS Code extensions (GUI mode only) ----
    code --install-extension ms-vscode.cpptools --force
    code --install-extension ms-vscode.cpptools-extension-pack --force
    code --install-extension eamodio.gitlens --force

    # ---- Optional: Desktop utilities (if using GUI mode) ----
    # Uncomment for GUI box:
    # sudo apt install -y gnome-terminal git

    # ---- Verify setup ----
    echo ">>> Python version: $(python --version)"
    echo ">>> G++ version: $(g++ --version | head -n 1)"
    echo ">>> VS Code version: $(code --version | head -n 1 || echo 'VS Code not installed (headless mode)')"
  SHELL
end
