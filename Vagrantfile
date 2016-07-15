# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.



  ANSIBLE_RAW_SSH_ARGS = []
  VAGRANT_VM_PROVIDER = "virtualbox"
  machine_box = "trusty-server-cloudimg-amd64-vagrant-disk1"
  machine_box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"

  zookeeper_node_count=3
  (1..zookeeper_node_count).each do |machine_id|
    ANSIBLE_RAW_SSH_ARGS << "-o IdentityFile=./.vagrant/machines/zookeeper#{machine_id}/#{VAGRANT_VM_PROVIDER}/private_key"
  end


  (1..zookeeper_node_count).each do |machine_id|
    config.vm.define "zookeeper#{machine_id}" do |machine|
      machine.vm.box = machine_box
      machine.vm.box_url = machine_box_url
      machine.vm.hostname = "zookeeper#{machine_id}"
      machine.vm.network "private_network", ip: "192.168.2.#{150+machine_id}"
      # machine.vm.synced_folder "provision/files/ssh/authorized_keys", "/home/spark/.ssh/authorized_keys", create:true
      machine.vm.provider "virtualbox" do |node|
          node.name = "zookeeper#{machine_id}"
          node.memory = 256
          node.cpus = 1
      end
      if machine_id == zookeeper_node_count
          machine.vm.provision :ansible do |ansible|
                  ansible.playbook = "provision/zookeeper.yml"
                  ansible.inventory_path = 'provision/inventory'
                  # ansible.verbose = "vvvv"
                  ansible.raw_ssh_args = ANSIBLE_RAW_SSH_ARGS
                  ansible.limit = 'zookeeper'
          end
      end
     end
  end


  ANSIBLE_RAW_SSH_ARGS_STORM = []
  storm_node_count=3
  (1..storm_node_count).each do |machine_id|
    ANSIBLE_RAW_SSH_ARGS_STORM << "-o IdentityFile=./.vagrant/machines/storm#{machine_id}/#{VAGRANT_VM_PROVIDER}/private_key"
  end
  (1..storm_node_count).each do |machine_id|
      config.vm.define "storm#{machine_id}" do |machine|
        machine.vm.box = machine_box
        machine.vm.box_url = machine_box_url
        machine.vm.hostname = "storm#{machine_id}"
        machine.vm.network "private_network", ip: "192.168.2.#{160+machine_id}"
        machine.vm.provider "virtualbox" do |node|
            node.name = "storm#{machine_id}"
            node.memory = 1024
            node.cpus = 1
        end
        if machine_id == zookeeper_node_count
            machine.vm.provision :ansible do |ansible|
                    ansible.playbook = "provision/storm.yml"
                    ansible.inventory_path = 'provision/inventory'
                    # ansible.verbose = "vvvv"
                    ansible.raw_ssh_args = ANSIBLE_RAW_SSH_ARGS_STORM
                    ansible.limit = 'storm'
            end
        end
       end
  end


  # ##storm nimbus
  # config.vm.define "storm-nimbus" do |node|
  #     node.vm.box = machine_box
  #     node.vm.box_url = machine_box_url
  #     node.vm.hostname = "storm-nimbus"
  #     node.vm.network "private_network", ip: "192.168.2.160"
  #     node.vm.network "forwarded_port", guest: 8080, host: 18080


  #     node.vm.provider "virtualbox" do |n|
  #         n.name = "storm-nimbus"
  #         n.memory = 512
  #         n.cpus = 1
  #     end

  #     node.vm.provision :ansible do |ansible|
  #         ansible.playbook = "provision/storm.yml"
  #         ansible.inventory_path = 'provision/inventory'
  #         ansible.raw_ssh_args = ANSIBLE_RAW_SSH_ARGS
  #         ansible.limit = 'storm'
  #     end
  # end


  # ##storm node
  # config.vm.define "storm1" do |node|
  #     node.vm.box = machine_box
  #     node.vm.box_url = machine_box_url
  #     node.vm.hostname = "storm1"
  #     node.vm.network "private_network", ip: "192.168.2.161"
  #     node.vm.network "forwarded_port", guest: 8080, host: 18080


  #     node.vm.provider "virtualbox" do |n|
  #         n.name = "storm1"
  #         n.memory = 512
  #         n.cpus = 1
  #     end

  #     node.vm.provision :ansible do |ansible|
  #         ansible.playbook = "provision/storm.yml"
  #         ansible.raw_ssh_args = ANSIBLE_RAW_SSH_ARGS
  #         ansible.inventory_path = 'provision/inventory'
  #         ansible.limit = 'storm'
  #     end
  # end

  # ##storm node
  # config.vm.define "storm2" do |node|
  #     node.vm.box = machine_box
  #     node.vm.box_url = machine_box_url
  #     node.vm.hostname = "storm2"
  #     node.vm.network "private_network", ip: "192.168.2.162"
  #     node.vm.network "forwarded_port", guest: 8080, host: 18080


  #     node.vm.provider "virtualbox" do |n|
  #         n.name = "storm2"
  #         n.memory = 512
  #         n.cpus = 1
  #     end

  #     node.vm.provision :ansible do |ansible|
  #         ansible.playbook = "provision/storm.yml"
  #         ansible.inventory_path = 'provision/inventory'
  #         ansible.raw_ssh_args = ANSIBLE_RAW_SSH_ARGS
  #         ansible.limit = 'storm'
  #     end
  # end



end
