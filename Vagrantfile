# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

require "vagrant-openstack-provider"

Vagrant.configure("2") do |config|
  config.vm.box = "openstack"

  # Name of the ssh username of the instance
  config.ssh.username = "ubuntu"

  # Uncomment if you want to use your own keypair
  # config.ssh.private_key_path = " "

  # Uncomment if the image is Cirros
  # config.ssh.shell = "/bin/sh"
  
  config.vm.provider "openstack" do |os|
    os.openstack_auth_url = "#{ENV['OS_AUTH_URL']}/tokens"
    os.openstack_network_url = "https://go.soneracloud.fi:9696/v2.0"
    os.openstack_volume_url = "https://go.soneracloud.fi:8776/v2/02fa5e2d0a904179849f37de3e32eb36"
    os.username = ENV['OS_USERNAME']
    os.password = ENV['OS_PASSWORD']  
    os.tenant_name = ENV['OS_TENANT_NAME']
    os.region = ENV['OS_REGION_NAME']

    # Specify instance information
    # These needs modifying
    os.flavor = "sonera.linux.small"
    os.image = "ubuntu-14.04.4"
    os.floating_ip_pool = "ext-net"
    # Uncomment if a specific IP is preferred 
    # os.floating_ip = "X.X.X.X"
    os.server_name = "vagrant-ubuntu"
    # If there are multiple available networks and security groups,
    # it will be necessary to specify the wanted ones using their names or ids (preferred)
    os.security_groups = ["cloudytest-sg"] 
    os.networks = ["cloudytest-nw"]
    # Uncomment if you want to use your own keypair
    # os.keypair_name = " " 
    # Uncomment if you want to attach a volume/volumes to the VM
    # os.volumes = [{name: " ", device: "/dev/vdb"}]
  end
end
