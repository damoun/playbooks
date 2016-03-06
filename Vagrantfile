Vagrant.require_version ">= 1.7.0"

$openbsd_install_python = <<SCRIPT
export "PKG_PATH=http://mirror.dalenys.com/pub/OpenBSD/5.8/packages/amd64/"
doas pkg_add -i python-2.7.10
SCRIPT

Vagrant.configure(2) do |config|

  if ENV['VAGRANT_MASTER01'] == '1'
    config.vm.define "master01" do |master01|
      master01.vm.hostname = "master01"
      master01.vm.box = "boxcutter/openbsd58"
      master01.ssh.sudo_command = "doas %c"
      master01.vm.network "private_network", ip: "192.168.57.2"
      master01.vm.provision "shell", inline: $openbsd_install_python
      master01.vm.provision "ansible", run: "always" do |ansible|
        ansible.verbose = "vv"
        ansible.inventory_path = "inventories/development"
        ansible.limit = 'all'
        ansible.playbook = "site.yml"
      end
    end
  end

end
