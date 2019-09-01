# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
   config.vm.box = "ubuntu/xenial64"
  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", 256]
  end

  config.vm.define :drupal, primary: true do |drupal_config|

    drupal_config.vm.hostname = 'drupal'
    drupal_config.vm.network :private_network, ip: "192.168.1.1"
    drupal_config.vm.provision "file", source: "~/playbook.zip", destination: "/tmp/"
    drupal_config.vm.provision :shell, inline: <<-SHELL
	  apt-get ansible git -y --nogpgcheck
  ansible-pull -i inventory -U https://github.com/sudharsanpunniyakotti/Alation  playbook.yml -e 'host_name=localhost, playbooks=haproxy'
  SHELL
  end
end
