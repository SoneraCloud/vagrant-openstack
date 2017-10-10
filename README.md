vagrant-openstack
========================

A demo on using [Vagrant](http://www.vagrantup.com/) to boot up an instance in an
OpenStack cloud regardless of OpenStack Keystone version that you are using.

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

Edit the ```instances.yml``` file with valid configurations for your OpenStack instance.
You can have multiple ready-made networks, volumes, and security groups attached to your
VM by providing either ids or names.

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
a new one, Vagrant will complain. The solution is to delete the .vagrant subdirectory
then run the command ```vagrant openstack reset```.

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
