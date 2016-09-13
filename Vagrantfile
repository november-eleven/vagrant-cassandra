# -*- mode: ruby -*-
# vi: set ft=ruby :

servers = []
(0..4).each do |i|
  name = 'node' + i.to_s
  ip = '10.11.66.' + (100 + i).to_s
  port = 7000 + i
  servers << {'name' => name, 'ip' => ip, 'port' => port}
end

Vagrant.configure("2") do |config|

  config.vm.box = "debian/jessie64"

  servers.each do |server|
    config.vm.define server['name'] do |c|

      c.vm.hostname = server['name']

      c.vm.network :forwarded_port, guest: 9042, host: server['port']
      c.vm.network :private_network, ip: server['ip']

      c.vm.provision :shell, path: "bootstrap"

      c.vm.provider "virtualbox" do |vb|
        vb.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
        vb.customize ["modifyvm", :id, "--cpus", "1"]
        vb.customize ["modifyvm", :id, "--memory", "512"]
      end

    end
  end

end
