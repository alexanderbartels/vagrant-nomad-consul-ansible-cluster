# -*- mode: ruby -*-
# # vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # always use Vagrants insecure key
  config.ssh.insert_key = false

  # Setup virtual machine box. This VM configuration code is always executed.
  config.vm.box = "hfm4/centos7"

 ## setup frontend servers
 config.vm.define "frontend-01" do |machine|
     machine.vm.network "private_network", ip: "192.168.33.10"
     machine.vm.hostname = 'frontend-01'
     machine.vm.provision "shell", inline:
       'echo "192.168.33.10 frontend-01" > /etc/hosts'

 end

# config.vm.define "frontend-02" do |machine|
#     machine.vm.network "private_network", ip: "192.168.33.11"
#     machine.vm.hostname = 'frontend-02'
#     machine.vm.provision "shell", inline:
#       'echo "192.168.33.11 frontend-02" > /etc/hosts'
# end

 ## setup mittletier servers
 config.vm.define "mittletier-01" do |machine|
     machine.vm.network "private_network", ip: "192.168.33.30"
     machine.vm.hostname = 'mittletier-01'
     machine.vm.provision "shell", inline:
       'echo "192.168.33.30 mittletier-01" > /etc/hosts'

 end

# config.vm.define "mittletier-02" do |machine|
#     machine.vm.network "private_network", ip: "192.168.33.31"
#     machine.vm.hostname = 'mittletier-02'
#     machine.vm.provision "shell", inline:
#       'echo "192.168.33.31 mittletier-02" > /etc/hosts'
# end

 ## setup control servers
 config.vm.define "control-01" do |machine|
     machine.vm.network "private_network", ip: "192.168.33.50"
     machine.vm.hostname = 'control-01'
     machine.vm.provision "shell", inline:
       'echo "192.168.33.50 control-01" > /etc/hosts'

     machine.vm.provision "ansible" do |ansible|
       ansible.verbose = "v"
       ansible.playbook = "./ansible/playbook.yml"
       ansible.host_key_checking = 'true'
       ansible.ask_sudo_pass = 'true'
       ansible.limit = 'all'
       ansible.groups = {
         "control_nodes" => ["control-01"],
         "frontend_nodes" => ["frontend-01"],
         "mittletier_nodes" => ["mittletier-01"]
       }
    end
 end

# config.vm.define "control-02" do |machine|
#     machine.vm.network "private_network", ip: "192.168.33.51"
#     machine.vm.hostname = 'control-02'
#     machine.vm.provision "shell", inline:
#       'echo "192.168.33.51 control-02" > /etc/hosts'
# end

 config.vm.provider :virtualbox do |v|
   v.linked_clone = true
   v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
   v.customize ["modifyvm", :id, "--memory", 1024]
   v.customize ["modifyvm", :id, "--cpus", 1]
   v.customize ["modifyvm", :id, "--ioapic", "on"]
   v.customize ["modifyvm", :id, "--rtcuseutc", "off"]
 end

 config.vm.provision "shell", inline:
   'sudo sed -ri "s/%admin ALL=NOPASSWD: ALL/%admin ALL=(ALL) NOPASSWD: ALL/" /etc/sudoers'

 config.vm.provision "shell", inline:
   'sudo yum -y update'

 config.ssh.forward_agent = true
end
