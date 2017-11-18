# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile for pleroma
# https://github.com/argrath/pleroma-vagrant
Vagrant.configure("2") do |config|
  config.vm.box = "debian/contrib-stretch64"
  config.vm.network "public_network", ip: "192.168.1.202"
  config.vm.synced_folder "data", "/vagrant"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

# See https://git.pleroma.social/pleroma/pleroma/wikis/Installing-on-Debian-Based-Distributions
$provision = <<SCRIPT
# add sources.list for elixir
wget https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb
sudo dpkg -i erlang-solutions_1.0_all.deb

# update package list
sudo apt-get update

# install elixir-related packages
sudo apt-get -y install esl-erlang
sudo apt-get -y install elixir

# install other packages
sudo apt-get install -y postgresql-9.6 build-essential git

# create database
sudo -u postgres psql -f /vagrant/pgsql.txt

# get source
git clone https://git.pleroma.social/pleroma/pleroma.git

# install dependencies
cd pleroma
mix local.hex --force
mix deps.get

# copy config
cp /vagrant/config.exs config
cp /vagrant/dev.secret.exs config

# migrate
mix local.rebar --force
mix ecto.migrate

# copy startup script
cp /vagrant/startup.sh ~
SCRIPT

  config.vm.provision "shell", inline: $provision, privileged: false

end
