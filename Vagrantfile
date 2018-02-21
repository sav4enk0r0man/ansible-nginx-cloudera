# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant::DEFAULT_SERVER_URL.replace('https://vagrantcloud.com')
VAGRANTFILE_API_VERSION = "2"
VM_NAME = "nginx-cloudera"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "comiq/dockerbox"

  config.vm.define VM_NAME do |v|
    v.vm.hostname = VM_NAME
    v.vm.network :private_network, ip: "10.1.13.1"
    config.vm.provider :virtualbox do |vb|
      vb.name = VM_NAME
      vb.memory = 512
      vb.cpus = 1
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      vb.customize ["modifyvm", :id, "--ioapic", "on"]
    end
  end

  # Provision ansible
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "vagrant-playbook.yml"
    ansible.host_key_checking = false
    ansible.sudo = true
    ansible.verbose = ENV['ANSIBLE_VERBOSE'] ||= "vvvv"
    ansible.tags = ENV['ANSIBLE_TAGS'] ||= "all"

    ansible.extra_vars = {
        ansible_ssh_user: 'vagrant',
        ansible_connection: 'ssh',
        ansible_ssh_args: '-o ForwardAgent=yes'
    }
    ansible.raw_ssh_args = ['-o UserKnownHostsFile=/dev/null']
    ansible.groups = {
      "servers" => [ VM_NAME ],
    }
  end

end
