Vagrant.require_version ">= 1.7.0"

$openbsd_install_python = <<SCRIPT
echo "nameserver 8.8.8.8" >> /etc/resolv.conf
export "PKG_PATH=http://mirror.dalenys.com/pub/OpenBSD/$(uname -r)/packages/$(uname -p)/"
pkg_add -i python-2.7.12
echo "permit nopass keepenv vagrant as root" > /etc/doas.conf
SCRIPT

Vagrant.configure(2) do |config|

  if ENV['VAGRANT_NS01'] == '1'
    config.vm.define "ns01" do |ns01|
      ns01.vm.hostname = "ns01"
      ns01.vm.box = "trombik/ansible-openbsd-6.0-amd64"
      #ns01.ssh.sudo_command = "doas %c"
      ns01.vm.network "forwarded_port", guest: 22, host: 2201
      ns01.vm.provision "shell", inline: $openbsd_install_python
      ns01.ssh.insert_key = false
    end
  end

  if ENV['VAGRANT_NS02'] == '1'
    config.vm.define "ns02" do |ns02|
      ns02.vm.hostname = "ns02"
      ns02.vm.box = "trombik/ansible-openbsd-6.0-amd64"
      #ns02.ssh.sudo_command = "doas %c"
      ns02.vm.network "forwarded_port", guest: 22, host: 2202
      ns02.vm.provision "shell", inline: $openbsd_install_python
      ns02.ssh.insert_key = false
    end
  end

end
