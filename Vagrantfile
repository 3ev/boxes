# vim: syntax=ruby

require 'yaml'

settings = YAML::load(File.read(File.dirname(__FILE__) + "/settings.yaml"))

Vagrant.configure(2) do |config|

  # Set the box to use

  config.vm.box = "3ev/" + settings["box"]

  # Hostname

  config.vm.hostname = settings["box"] + ".dev"

  # Default private networking IP

  config.vm.network :private_network, ip: settings["ip"]

  # Synced folders

  config.vm.synced_folder settings["sites_path"], "/var/www/vhosts", id: "vagrant-root", nfs: true

  # Use host SSH

  config.ssh.insert_key = false
  config.ssh.forward_agent = true

  # Override default SSH port

  config.vm.network "forwarded_port", guest: 22, host: settings["ssh_port"], id: "ssh"

  # Virtualbox config (1.5GB RAM by default and some networking settings)

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", settings["ram"]]
    v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end
end
