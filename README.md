vagrant-openstack
========================

This demo is used for booting up a single instance in an OpenStack cloud with
[Vagrant](http://www.vagrantup.com/) regardless of OpenStack Keystone version that you are using.

Prerequisites
-----------

Vagrant (you can get the latest version from http://www.vagrantup.com/), OpenStack
credential file, and [vagrant-openstack-provider](https://github.com/ggiamarchi/vagrant-openstack-provider)
plugin

```
$ vagrant plugin install vagrant-openstack-provider
```

Usage
-----------

```instances.yml``` contains the instance-specific configurations for the instance that will be
created. You **must** edit this file.
- The demo assumes your OpenStack keypair is named the same as the local account that you are using,
and you have an SSH keypair named id_rsa*. But you can override them as well as flavor, image, etc.
with this file.
- The vagrant-openstack-provider plugin has a Neutron bug which always assumes Neutron API
uses *http* instead of *https*. The solution is to tell Vagrantfile to use the right API URL
followed by ```/v2.0```, for example, ```https://network.fi-1.nebulacloud.fi:9696/v2.0```.
- The list of security groups is empty in this file, so adding security group(s) is a minimum
requirement to get this demo working.

It's possible to attach multiple ready-made networks, volumes, and security groups to your VM by
providing either their ids (preferred) or names; they should be inside ' ' or " " and separated
by commas.

Start up the VM:
```
$ vagrant up
```

Connect to the VM via SSH:
```
$ vagrant ssh
```

Shut down the VM:

```
$ vagrant halt
```

Destroy the VM:
```
$ vagrant destroy
```

If you don't terminate your VM with ```vagrant destroy```, the next time you boot up
a new one, Vagrant will complain. The solution is to delete the ```.vagrant```
subdirectory then run the command ```vagrant openstack reset```.

Vagrant Subcommands
-----------

In addition to OpenStack CLIs, it's also possible to get the same kind of information
with Vagrant.
```
vagrant openstack <command>

Available subcommands:
- image-list
- flavor-list
- network-list
- subnet-list
- floatingip-list
- volume-list
- reset (Reset Vagrant OpenStack provider to a clear state)
```
