# -*- mode: ruby -*-
# vi: set ft=ruby :

API_VER = "2"

Vagrant.configure(API_VER) do |config|
  # gyptazy provides a good range of arm64 vagrant boxes for use with vmware_fusion
  config.vm.box = "gyptazy/rocky9.3-arm64"
  config.vm.hostname = "k8s-node-001"

  config.vm.provider "vmware_desktop" do |v|
    v.vmx["memsize"] = "2048"
    v.vmx["numvcpus"] = "2"
    # gui = true need for private network functionality to work
    v.gui = false
  end

  # Add an authorised a public key to each vagrant box
  config.vm.provision "shell" do |s|
    ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_vagrant.pub").first.strip
    s.inline = <<-SHELL
      echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
      echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
    SHELL
  end
end
