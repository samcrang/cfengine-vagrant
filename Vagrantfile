# -*- mode: ruby -*-
# # vi: set ft=ruby :

$provision = <<EOF
echo "deb http://cfengine.com/pub/apt $(lsb_release -cs) main" > /etc/apt/sources.list.d/cfengine-community.list
wget --output-document=/tmp/cfengine-gpg.key http://cfengine.com/pub/gpg.key
sudo apt-key add /tmp/cfengine-gpg.key
rm /tmp/cfengine-gpg.key
apt-get update
apt-get -y install cfengine-community
/var/cfengine/bin/cf-key
cp -Rp /var/cfengine/share/CoreBase /var/cfengine/masterfiles
/var/cfengine/bin/cf-agent --bootstrap `hostname -I`
EOF

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "debian-wheezy-x64-nocm"
  config.vm.box_url = "http://puppet-vagrant-boxes.puppetlabs.com/debian-70rc1-x64-vbox4210-nocm.box"
  config.vm.provision "shell", inline: $provision
end
