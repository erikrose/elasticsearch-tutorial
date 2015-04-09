# -*- mode: ruby -*-
# vi: set ft=ruby :

$package_repo = <<SCRIPT
wget -qO - https://packages.elasticsearch.org/GPG-KEY-elasticsearch | sudo apt-key add -
sudo add-apt-repository "deb http://packages.elasticsearch.org/elasticsearch/1.4/debian stable main"
aptitude update -y
SCRIPT

$install_and_start_elasticsearch = <<SCRIPT
aptitude install -y elasticsearch
sudo update-rc.d elasticsearch defaults 95 10
sudo /etc/init.d/elasticsearch start
/usr/share/elasticsearch/bin/plugin -i elasticsearch/marvel/latest
echo "binaries are in /usr/share/elasticsearch/bin"
SCRIPT


Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/trusty64"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"
  config.vm.box_download_checksum_type = "sha256"
  config.vm.box_download_checksum = "818412bd6b40f9823eb4630c75e6d4c3e0b9d80c51d84a34f226aa61bc64bb93"

  config.vm.provider "virtualbox" do |vb|
      vb.memory = "4096"
  end

  config.vm.network "forwarded_port", guest: 9200, host: 9200

  config.vm.provision "shell", inline: $package_repo
  config.vm.provision "shell", inline: "aptitude install -y default-jre"
  config.vm.provision "shell", inline: $install_and_start_elasticsearch

end
