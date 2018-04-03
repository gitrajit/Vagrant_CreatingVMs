# Vagrant_CreatingVMs
Vagrant to create multiple VMs including ansible control, DB, etc

# Prerequisite software
* Install Oracle VirtualBox or VMware
* Install Vagrant version 2.
* Download precise64.box from https://hashicorp-files.hashicorp.com/precise64.box

# Steps to Execute
```
[~]$ mkdir workingDir
[~]$ cd workingDir
[~]$ vagrant init hashicorp/precise64
```
### Replace the vagrantfile with this vagrantfile
```
[~]$ vagrant up

```

## To check the vagrant status
```
[~]$ vagrant status
```

## To destroy vagrant
```
[~]$ Vagrant destroy
```
