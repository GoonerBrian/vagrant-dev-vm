# vagrant-dev-vm
This is a Vagrantfile I'll be using for a dev env while I brush up on C++. I also installed Python because I want to study more advanced aspects of Python/Pandas to be more proficient at work.

## Setup Instructions
- [Install Vagrant](https://developer.hashicorp.com/vagrant/docs/installation)
- [Install VirtualBox](https://www.virtualbox.org/)
- Clone this repo
- Run `cd vagrant-dev-vm`
- Adjust `vb.memory` and `vb.cpus` as appropriate for you machine and comment/uncomment lines regarding GUI as needed
- Run ` vagrant up` to start the VM
- Once complete, run `vagrant ssh` to open a shell in the VM
- Run the following:
```
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

## VS Code Remote SSH: Connect to Host...
- Run `vagrant ssh` to reopen shell to VM or if still open, continue
- Create a `config` file (if one does not already exist) at `C:/Users/<username>/.ssh`
- Run `vagrant ssh-config` and copy/paste output into `config` file. This names the connection "default". Rename it if you like but I'll proceed assuming it is named "default"
- Open Command Palette (Ctrl+Shift+P)
- Search for "Remote SSH: Connect to Host..." and select it
- Select "default"
- This will open a new VS Code window (Your first time you may be asked additional questions. I created my `config` file during my initial connection but I think if I had created the `config` file in advance, that would have bypassed those questions since they would have been answered in the `config` file.)
- Select "Linux" from the dropdown
- You should now be connected to you VM