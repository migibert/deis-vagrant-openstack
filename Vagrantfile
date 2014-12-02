require 'vagrant-openstack-provider'

Vagrant.configure('2') do |config|

  config.ssh.username = ENV['OS_SSH_USERNAME']
  config.ssh.private_key_path = ENV['OS_KEYPAIR_PATH']

  config.vm.provider :openstack do |os|
    os.username           = ENV['OS_USERNAME']
    os.password           = ENV['OS_PASSWORD']
    os.flavor             = ENV['OS_FLAVOR']
    os.image              = ENV['OS_IMAGE']
    os.openstack_auth_url = ENV['OS_AUTH_URL']
    os.tenant_name        = ENV['OS_TENANT_NAME']
    os.keypair_name       = ENV['OS_KEYPAIR_NAME']
    os.sync_method        = 'none'
  end

  (1..3).each do |i|
    config.vm.define "instance_#{i}" do |instance|
      instance.vm.provider :openstack do |os|
        os.server_name      = "deis-#{i}"
        os.networks         << ENV['OS_NETWORK_NAME']
        os.user_data = File.open("cloud-config.yml", "rb").read
      end
    end
  end
end




