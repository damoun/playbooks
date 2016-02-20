Vagrant.require_version ">= 1.7.0"

$openbsd_install_python = <<SCRIPT
export "PKG_PATH=http://mirror.dalenys.com/pub/OpenBSD/5.8/packages/amd64/"
doas pkg_add -i python-2.7.10
SCRIPT

Vagrant.configure(2) do |config|

  if ENV['VAGRANT_DNS01'] == '1'
    config.vm.define "dns01" do |dns01|
      dns01.vm.hostname = "dns01"
      dns01.vm.box = "boxcutter/openbsd58"
      dns01.ssh.sudo_command = "doas %c"
      dns01.vm.network "private_network", ip: "192.168.57.2"
      dns01.vm.provision "shell", inline: $openbsd_install_python
      dns01.vm.provision "ansible", run: "always" do |ansible|
        ansible.verbose = "vv"
        ansible.inventory_path = "inventories/development"
        ansible.limit = 'all'
        ansible.playbook = "site.yml"
      end
    end
  end

end
