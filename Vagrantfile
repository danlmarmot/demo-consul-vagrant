# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

    # Virtualbox settings
    # set nprocs to 2; consul can block badly with just one
    config.vm.provider "virtualbox" do |v|
        v.memory = 1024
        v.cpus = 2
    end

    # Common settings that all VMs share
    config.vm.synced_folder "shared", "/home/vagrant/shared"
    config.vm.box = "ubuntu/trusty64"

    # Define two VMs, but don't provision them yet

    #  We are using static IP addresses from the 10.10.10/24 CIDR block
    #    though in real life these should be assigned via DHCP
    #  The Ansible provisioning scripts do need to know this CIDR block,
    #    and this CIDR block is defined in the file group_vars/all

    config.vm.define "db0" do |db0|
        db0.vm.network "private_network", ip: "10.10.10.10"
        # Open port 8500 for Consul UI
        db0.vm.network :forwarded_port, guest: 8500, host: 8500
    end

    config.vm.define "db1" do |db1|
        db1.vm.network "private_network", ip: "10.10.10.11"
    end

    # Define a third VM--and run Ansible only on this very last one
    #   This is done so that all VM host info is known to Ansible,
    #   including dynamic facts such as IP addresses
    config.vm.define "db2" do |db2|
        db2.vm.network "private_network", ip: "10.10.10.12"

        db2.vm.provision "ansible" do |ansible|
            ansible.extra_vars = "@group_vars/vagrant"
            ansible.groups= {
                    "vagrant" => ["db0", "db1", "db2"]
            }
            ansible.verbose = "v"
            ansible.playbook = "consul.yml"
            ansible.limit = "all"
            ansible.raw_arguments = "-i .vagrant/provisioners/ansible/inventory/vagrant_ansible_inventory"
        end
    end

end