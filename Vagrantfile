# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'vagrant-openstack-provider'
require 'yaml'

VAGRANTFILE_API_VERSION = '2'
ENV['VAGRANT_DEFAULT_PROVIDER'] = 'openstack'

api_version = ENV['OS_IDENTITY_API_VERSION']

dir = File.dirname(File.expand_path(__FILE__))
instances = YAML.load_file("#{dir}/instances.yml")
whoami = ENV['USER']
hostname = "vagrant-#{whoami}"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.hostname = hostname
  config.ssh.username = whoami
  config.ssh.private_key_path = instances['private_key']
  # CirrOS uses /bin/sh instead of bash, so uncomment the following line if you're
  # using CirrOS image
  # config.ssh.shell = instances['shell']

  config.vm.provider "openstack" do |os|
    os.openstack_auth_url = ENV['OS_AUTH_URL']
    os.openstack_network_url = instances['neutron_api_url']
    os.username = ENV['OS_USERNAME']
    os.password = ENV['OS_PASSWORD']
    os.region = ENV['OS_REGION_NAME']
    if api_version == '3'
      os.project_name = ENV['OS_PROJECT_NAME']
      os.domain_name = ENV['OS_USER_DOMAIN_NAME']
      os.identity_api_version = api_version
    else
      os.tenant_name = ENV['OS_TENANT_NAME']
    end

    os.flavor = instances['flavor']
    os.image = instances['image']
    os.floating_ip_pool = instances['external_network']
    # It's possible to use a predefined floating IP with the following line uncommented
    # os.floating_ip = instances['floating_ip']
    os.server_name = hostname
    os.security_groups = instances['security_groups']
    os.networks = instances['networks']
    if instances['keypair_name'] != ''
      os.keypair_name = instances['keypair_name']
    else
      os.keypair_name = whoami
    end
    os.volumes = instances['volumes']
    os.availability_zone = instances['availability_zone']
    os.user_data = "#cloud-config:
      system_info:
        default_user:
          name: #{whoami}
    "
    os.sync_method = 'none'
  end
end
