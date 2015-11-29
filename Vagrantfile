# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure("2") do |config|
  config.vm.box = "radiant_new"
  config.vm.box_url = "/home/hofid/vagrant_box/ubuntu-14.04-amd64.box"

  config.vm.hostname = "radiant"
  config.vm.network :forwarded_port, guest: 22, host: 2255, id: 'ssh'
  config.ssh.port = 2255
  config.ssh.insert_key = false

  # port forward nginx
  config.vm.network :forwarded_port, guest: 80,   host: 8888

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network :private_network, ip: "10.10.10.33"

  # If true, then any SSH connections made will enable agent forwarding.
  # Default value: false
  config.ssh.forward_agent = true

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  config.vm.synced_folder ".", "/radiant",          disabled: false, type: "nfs"


  config.vm.provider :virtualbox do |vb|
    # Don't boot with headless mode
    # vb.gui = true

    # Use VBoxManage to customize the VM. For example to change memory:
    vb.customize ["modifyvm", :id, "--memory",  "1024"]
    vb.customize ["modifyvm", :id, "--acpi",    "on"]
    vb.customize ["modifyvm", :id, "--ioapic",  "on"]
    vb.customize ["modifyvm", :id, "--cpus",  "2"]
  end

#  #config.vm.provision :shell, path: 'scripts/vm_provision.sh'
#  config.vm.provision "ansible" do |ansible|
#    ansible.host_key_checking = false
#    ansible.playbook = "../../provisioning/vagrant-medusa.yml"
#    ansible.limit = 'all'
#    ansible.inventory_path = "../../provisioning/inventory/vagrant/vagrant-medusa"
#    ansible.extra_vars = "../../provisioning/env/vagrant-medusa.json"
#    ansible.verbose = 'vv'
#  end

end
