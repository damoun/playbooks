Vagrant.require_version ">= 1.7.0"

$openbsd_install_python = <<SCRIPT
echo "nameserver 8.8.8.8" >> /etc/resolv.conf
export "PKG_PATH=http://mirror.dalenys.com/pub/OpenBSD/$(uname -r)/packages/$(uname -p)/"
pkg_add -i python-2.7.11
echo "permit nopass keepenv vagrant as root" > /etc/doas.conf
SCRIPT

Vagrant.configure(2) do |config|

  if ENV['VAGRANT_MASTER01'] == '1'
    config.vm.define "master01" do |master01|
      master01.vm.hostname = "master01"
      master01.vm.box = "kaorimatz/openbsd-5.9-amd64"
      #master01.ssh.sudo_command = "doas %c"
      master01.vm.network "private_network", ip: "192.168.57.2"
      master01.vm.provision "shell", inline: $openbsd_install_python
      master01.ssh.insert_key = false
    end
  end

  if ENV['VAGRANT_SLAVE01'] == '1'
    config.vm.define "slave01" do |slave01|
      slave01.vm.hostname = "slave01"
      slave01.vm.box = "kaorimatz/openbsd-5.9-amd64"
      #slave01.ssh.sudo_command = "doas %c"
      slave01.vm.network "private_network", ip: "192.168.57.3"
      slave01.vm.provision "shell", inline: $openbsd_install_python
      slave01.ssh.insert_key = false
    end
  end

end
