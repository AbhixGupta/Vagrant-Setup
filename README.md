
# About Vagrant

Vagrant is an open source tool/software which is being to easily provision and configure the virtual environment. It gets easily integrated with Virtualbox, Vmware and docker, the major difference between these virtulization software and vagrant is that, vagrant allows user to easily modiy or change the virtulization environment of Virtual Machine by using the simple, customizable API to mange that machine at any instance.

Vagrant currently supports the Windows, Mac, FreeBSD and Linux operating systems. This tool is built using the ruby language and have currently under MIT licence.

### Poblem with virtual machines
* To install the operating system in virtual machine we have download the iso image of other file in order spin up that machine.
* To install run the virtual machine form the iso images very time consuming.
* To install these machines all resorces and configuration setup have to done manually.
* The real problem when we have to replicate or run the multiple virtual machine parallelly, your system becomes slow and machine resource consumption becomes high even for small tasks.


## Vagrant Features
Vagrant offers list of rich features with fleblity and allows user to manage their virtual machines through command line interface and thorugh vagrantfile.

* Vagrantfile:  Vagrant configuration file that uses ruby to write scipts to manage the virtual machines.
* Boxes: It is similar to the vagrantfile, but it's a kind of package that contains that ability to be shared and available on vagrant cloud, or  we say it act as a template.
* Networking: Vagrant supports three kinds of Networking which includes, Port Forwarding, Private and Public Networking.
* Provisioning: It allows user to provision and manage the vagrant machines using the configuration management tools like Chef, Ansible, Puppet etc. Docker, shell scipting can also be used to provision the virtual machines.
* Plugins: Plugins provides addional funtionality to manage and configre the virtual machines.

# Installation
Install Virtuabox and Vagrant in windows by downloading it from its offcial website.
Note: Kindly install virtualbox before Vagrant.

Here we are using the centos 7 image is named as "centos/7" box in vagrant box cloud. For running any os virtual machine you have to go Vagrant box website to check the name of that operating system you want to use.

```bash
  vagrant init centos/7
  vagrant up
  vagrant ssh
  cat /etc/os-release
  sudo -i
  whoami
```
To close the vm 
```bash
  vagrant halt
```
To delete the vm 
```bash
  vagrant destroy
```
To delete the vm 
```bash
  vagrant destroy
```
To check all available Boxes 
```bash
  vagrant box list -i
  vagrant global-status
```
Adding the bridge network in the virtual machine.
```bash
  Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/bionic64"
    config.vm.network "public_network"
  end
```
Add ssh to system to enable login from any location in computer. Login into vagrant machine
```bash
  useradd dev
  passwd dev  //enter the password
  vi /etc/ssh/sshd_config
  PasswordAuthentication = yes (save and exit)
  service ssh restart
```
Exit the vagrant machine and login through ssh using 
```bash
  ssh dev@privateIP
```
To run the customize the RAM and CPU, use and modify the below command accordingly.
```bash
  Vagrant.configure("2") do |config|
    config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    vb.cpus = 2
  end
```

Sync Directory between vagrant machine and host machine. By deafult its path is "/vagrant => D:/Vagrant/ubuntu", where /vagrant is directory in your vagrant machine and other side is your wiinodws direcory location.
Sync directory maintains that data on both host and vagrant machine. To change this directory change the path in "vagrantfile".

Modificaiton in file for installing git inside the vagrant machine (for Linux).
```bash
config.vm.provision "shell", inline: <<-SHELL
     apt-get update
     apt-get install -y git
   SHELL
```
This is how you run multiple commands only by making modifications in vagrant file.

Now lets see how we can make multiple virtual machine from single vagrantfile.

```bash
Vagrant.configure("2") do |config|
  config.vm.provision "shell", inline: "echo Hello first machine"
  config.vm.network "public_network"

  config.vm.define "u18" do |u18|
    u18.vm.box = "ubuntu/bionic64"
    config.vm.provider "virtualbox" do |vb|
    vb.memory = "1048"
    vb.cpus = 1
  end
  end

  config.vm.define "u16" do |u16|
    u16.vm.box = "ubuntu/xenial64"
    config.vm.provider "virtualbox" do |vb|
    vb.memory = "1048"
    vb.cpus = 1
   end
  end
end

```
### Changing the dis size of the Virtual Machine
To change the disk size of the virtual machine we need to install one plugin
```bash
  vagrant plugin install vagrant-disksize
```
Now add the following in your Vagrantfile to increase the disk size by runnign following commands. The only limitation is that, it works only with the Virtualbox. Second the disk can only be incresed and vice-versa is not possible.
```bash
  Vagrant.configure('2') do |config|
  config.vm.box = 'ubuntu/bionic64'
  config.disksize.size = '25GB'
end
```
### Communication between different Machines.
To establish a communication between different running virtual machines we need to install Vagrant hostmanager Plugin. This helps the machine on the same network to communicate with their hostname. Make sure to add correct IP addresses in the file.
```bash
  vagrant plugin install vagrant-hostmanager
```
Enable the hostmanger plugin into your Vagrantfile.
```bash
  Vagrant.configure('2') do |config|
  config.hostmanager.enabled = true
  config.vm.box = 'ubuntu/bionic64'
  config.disksize.size = '25GB'
end
```
For multiple machines.
```bash
Vagrant.configure("2") do |config|
  config.vm.provision "shell", inline: "echo Hello first machine"
  config.hostmanager.enabled = true
  config.vm.network "public_network"

  config.vm.define "u18" do |u18|
    u18.vm.box = "ubuntu/bionic64"
    u18.vm.hostname = "u18.example.com
    u18.vm.network "private_network", ip: "172.16.48.12"
    config.vm.provider "virtualbox" do |vb|
    vb.memory = "1048"
    vb.cpus = 1
  end
  end

  config.vm.define "u16" do |u16|
    u16.vm.box = "ubuntu/xenial64"
    u16.vm.hostname = "u16.example.com"
    u18.vm.network "private_netwrok", ip: "172.16.48.13"
    config.vm.provider "virtualbox" do |vb|
    vb.memory = "1048"
    vb.cpus = 1
   end
  end
end

```

