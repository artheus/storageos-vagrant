# -*- mode: ruby -*-
# vi: set ft=ruby :
#
#

Vagrant.require_version ">= 1.9.3"

nodes = 3

vmmemory = 2048
vmcpus = 2

nodeNames = nodes.times.collect { |n| "storageos-#{n+1}" }
nodeIpList = nodes.times.collect { |n| "172.28.128.#{n+5}" } # 172.28.128.5 -> 172.28.128.N

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  (0..nodes-1).each do |nodeid|
    config.vm.define nodeNames[nodeid] do |node|

      node.vm.hostname = nodeNames[nodeid]
      node.vm.network "private_network", ip: nodeIpList[nodeid]

      node.vm.provider "virtualbox" do |v|
        v.memory = vmmemory
        v.cpus = vmcpus
      end

      if nodeid+1 == nodes
        node.vm.provision :ansible do |ansible|
          ansible.limit = "all"
          ansible.become = true
          ansible.become_user = "root"
          ansible.playbook = "site.yaml"

          ansible.raw_arguments = ["--connection=paramiko"]
          ansible.host_vars = Hash[nodeNames.zip(nodeIpList.map{ |ip| Hash["advertise_ip", ip] })]
          ansible.extra_vars = {
            join_list: "#{nodeIpList.join(':5705,')}:5705"
          }
        end
      end
    end
  end
end
