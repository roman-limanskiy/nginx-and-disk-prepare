ENV['VAGRANT_EXPERIMENTAL'] = "disks"

Vagrant.configure("2") do |config|

  config.vm.provider :virtualbox do |v|
    v.memory = 512
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "user.yml"
  end

  config.vm.define "webserver-01" do |webserver|
    webserver.vm.box = "ubuntu/xenial64"
    webserver.vm.hostname = "webserver-01"
    webserver.vm.disk :disk,
                       name: "extra_storage_1",
                       size: "256MB"
    webserver.vm.disk :disk,
                       name: "extra_storage_2",
                       size: "256MB"
    webserver.vm.network :public_network,
                          bridge: "wlx00e04c0a3bbc",
                          ip: "192.168.0.71"
  end

  config.vm.define "webserver-02" do |webserver|
    webserver.vm.box = "ubuntu/xenial64"
    webserver.vm.hostname = "webserver-02"
    webserver.vm.disk :disk,
                       name: "extra_storage_1",
                       size: "256MB"
    webserver.vm.disk :disk,
                       name: "extra_storage_2",
                       size: "256MB"
    webserver.vm.network :public_network,
                          bridge: "wlx00e04c0a3bbc",
                          ip: "192.168.0.72"
  end
end
