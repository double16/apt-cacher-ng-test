# -*- mode: ruby -*-
# vi: set ft=ruby :

cache = ENV['APT_CACHE'] || "http://169.254.169.254:3142"

Vagrant.configure("2") do |config|

  config.vm.define "centos" do |centos|
    centos.vm.box = "bento/centos-7.5"
  end

  config.vm.define "fedora" do |fedora|
    fedora.vm.box = "generic/fedora28"
    fedora.vm.provision "shell", inline: <<-SHELL
      echo 'proxy=#{cache}' >> /etc/dnf/dnf.conf
    SHELL
  end

  config.vm.define "ubuntu" do |ubuntu|
    ubuntu.vm.box = "ubuntu/bionic64"
    ubuntu.vm.provision "shell", inline: <<-SHELL
      echo -e 'Acquire::HTTP::Proxy "#{cache}";\nAcquire::HTTPS::Proxy "false";' >> /etc/apt/apt.conf.d/01proxy
    SHELL
  end

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.cpus = 1
    vb.memory = 512
  end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    echo 'proxy=#{cache}' >> /etc/yum.conf
  SHELL
end
