# vagrant-openstack


## Overview

Vagrant, an open-source product, is best described as a Virtual Machine manager. It is a popular 
automation framework that helps you build development and testing environments. You can easily deploy those 
to the cloud by using the Vagrant OpenStack plugin.  

Vagrant talks to the providers (VirtualBox, VMware, Hyper-V, OpenStack, etc.) and automatically spins up 
multiple virtual machines, each with their own configurations managed by Puppet, Chef, etc.

Vagrant is written in Ruby, but a Vagrantfile is easy to understand without knowing Ruby.

Vagrant can handle the entire lifecycle of development machines:
- SSH, suspend, halt, resume.
- Detroy, delete metadata, rebuild.
- Package up your machines' entire state and redistribute them to other development members.

Our demo helps deploy a single test instance, but the integration provided by the plugin supports far more.

## Prerequisites

- Vagrant installed on local machine.
- The OpenStack credential file downloaded from the dashboard.
- The plugin vagrant-openstack-provider.

```$ vagrant plugin install vagrant-openstack-provider```

## Vagrant up

All you need to do manually is to create your own network if it is not available yet.

Sourcing the credential file, then specifying OpenStack as the provider.

```$ vagrant up --provider=openstack```

Connecting via SSH to the VM.

```$ vagrant ssh```

Shutting down the VM.

```$ vagrant halt```

We should use ```vagrant destroy``` instead of terminating the instance from the dashboard, otherwise Vagrant will complain.

```$ vagrant destroy```

## Vagrantfile Parameters

###Standard Parameters
```private_key_path```, ```ssh.username```, ```ssh.port```

###Credentials

```username```, ```password```, ```tenant_name```, ```region```, ```openstack_auth_url```, 
```openstack_compute_url```, ```openstack_network_url```, ```openstack_volume_url```, 
```openstack_image_url```, ```endpoint_type```

###Instance Parameters

```server_name```, ```flavor```, ```image```, ```availability_zone```, ```security_groups```, 
```floating_ip```, ```floating_ip_pool```, ```networks```, ```volumes```,  ```stacks```, ```keypair_name```

## Vagrant Subcommands

Vagrant subcommands are useful to find out information about images, flavors, networks, etc. instead 
of using OpenStack commands.
 
```
vagrant openstack

Subcommands:
- image-list
- flavor-list
- network-list
- subnet-list
- floatingip-list
- volume-list
- reset: Reset Vagrant OpenStack provider to a clear state
```

## Vagrant on Windows

In order to source the credential file, you will need some tool like Cygwin instead of Command Prompt or Powershell.
 
Vagrant usually stores the private key in the default path C:/HashiCorp/Vagrant/{folder_name}/.vagrant/machines/default/virtualbox.

In order to SSH to the VM on Windows, that file needs converting to a .ppk file using PuTTYgen.

Then use that .ppk file in your PuTTY session: Connection > SSH > Auth > Private key file for authentication.

The host name is 127.0.0.1, the port is 2222, and the default username is 'vagrant'. 

## Limitations:

The Cirros image is a bit different from other Linux ones. It uses /bin/sh instead of bash, so you need to
comment out a specific line when you want to use Cirros.

And it will complain about the synced folder, but everything works fine. Vagrant can disable the synced 
folder when being used with VirtualBox, but that feature seems not to work with OpenStack.

