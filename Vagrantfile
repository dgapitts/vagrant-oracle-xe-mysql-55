# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant::Config.run do |config|

  config.vm.define :oraxe do |oxe_config|
    oxe_config.vm.box = "ubuntu-1110-server-amd64"
    oxe_config.vm.box_url = "http://timhuegdon.com/vagrant-boxes/ubuntu-11.10.box"
    oxe_config.vm.host_name = "oraxe"
    #oxe_config.vm.share_folder "tmp", "/tmp", "/tmp"
    oxe_config.vm.forward_port 22, 41022, :adapter => 1
    oxe_config.vm.network :hostonly, "33.33.33.12", :adapter => 2
    oxe_config.vm.provision :puppet, :module_path => "modules", :options => "--verbose --trace" do |puppet|
      puppet.manifests_path = "manifests"
      puppet.manifest_file  = "oracle-xe.pp"
    end
    oxe_config.vm.customize [ "modifyvm", :id, "--name", "ora-xe" ,"--memory", "2048"]
    oxe_config.vm.boot_mode = :gui
  end

  config.vm.define "mysql" do |mysql|
    mysql.vm.box = "precise64"
    mysql.vm.box_url = "http://files.vagrantup.com/precise64.box"
    mysql.vm.boot_mode = :gui
    mysql.vm.network :hostonly, "33.33.33.11"
    mysql.vm.host_name = "mysql"
    mysql.vm.provision :puppet do |puppet|
      puppet.manifests_path = "manifests"
      puppet.manifest_file = "mysql_server.pp"
    end
  end

end
