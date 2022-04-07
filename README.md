
# About Vagrant

Vagrant is an open source tool/software which is being to easily provision and configure the virtual environment. It gets easily integrated with Virtualbox, Vmware and docker, the major difference between these virtulization software and vagrant is that, vagrant allows user to easily modiy or change the virtulization environment of Virtual Machine by using the simple, customizable API to mange that machine at any instance.

Vagrant currently supports the Windows, Mac, FreeBSD and Linux operating systems. This tool is built using the ruby language and have currently licence under MIT licence.

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
## Vagrant's CPU and Memory
Vagrant's box comes up with default cpu, ram, storage size, but we can manipulate these settings by our needs. For this we have make an approprite changes in the vagrantfile.
```bash

```


## Vagrant Networking
How we can do port forwarding

