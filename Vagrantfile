# -*- mode: ruby -*-
# vi: set ft=ruby :
DOKKU_BOOTSTRAP_SCRIPT = "https://raw.githubusercontent.com/protonet/dokku/master/bootstrap.sh"
DOKKU_REPO = "https://github.com/protonet/dokku.git"
DOKKU_BRANCH = "master"

Vagrant::configure("2") do |config|
  config.ssh.forward_agent = true

  config.vm.box = "ubuntu/trusty64"
  config.vm.synced_folder File.dirname(__FILE__), "/var/lib/dokku/plugins/dokku-label"
  config.vm.network :private_network, ip: "10.42.42.42"

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    # Ubuntu's Raring 64-bit cloud image is set to a 32-bit Ubuntu OS type by
    # default in Virtualbox and thus will not boot. Manually override that.
    vb.customize ["modifyvm", :id, "--ostype", "Ubuntu_64"]
    vb.customize ["modifyvm", :id, "--memory", "2048"]
  end

  config.vm.provision :shell, :inline => "cd /tmp/ && wget #{DOKKU_BOOTSTRAP_SCRIPT}"
  config.vm.provision :shell, :inline => "cd /tmp/ && DOKKU_REPO=#{DOKKU_REPO} DOKKU_BRANCH=#{DOKKU_BRANCH} bash bootstrap.sh"
end
