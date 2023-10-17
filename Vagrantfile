# -*- mode: ruby -*-
# vi: set ft=ruby :
$box_image = "ubuntu/bionic64"
$install_docker = <<SCRIPT
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
SCRIPT
$launch_monitoring = <<SCRIPT
  git clone https://github.com/cristianpb/telegraf-influxdb-grafana-docker.git
  cd telegraf-influxdb-grafana-docker
  make up
SCRIPT

Vagrant.configure("2") do |config|

    config.vm.box = $box_image
    config.vm.provider "virtualbox" do |v|
      v.memory = 2048
      v.cpus = 2
    end
    config.vm.network "forwarded_port", :guest => 8083, :host => 8083
    config.vm.network "forwarded_port", :guest => 8086, :host => 8086
    config.vm.network "forwarded_port", :guest => 8090, :host => 8090
    config.vm.network "forwarded_port", :guest => 8099, :host => 8099
    config.vm.network "forwarded_port", :guest => 3000, :host => 3000
    config.vm.network "forwarded_port", :guest => 8888, :host => 8888
    
    config.vm.provision "shell", inline: <<-SHELL
        #{$install_docker}
        #{$launch_monitoring}
    SHELL
end    