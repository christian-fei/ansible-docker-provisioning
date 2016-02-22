Vagrant.configure('2') do |config|
  config.vm.box = 'ubuntu/trusty64'
  config.vm.hostname = 'pomodoro.dev'
  config.ssh.shell = 'bash -c \'BASH_ENV=/etc/profile exec bash\''

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--memory", 1024]
    vb.customize ["modifyvm", :id, "--cpus", 2]
  end

  config.vm.network :private_network, ip: "192.168.11.10"
  config.vm.network "forwarded_port", guest: 80, host: 8080

  config.vm.synced_folder "./", "/main", type: "nfs", :mount_options => ['nolock,vers=3,udp,noatime,actimeo=1']

  config.vm.provision :ansible do |ansible|
    ansible.inventory_path = "provisioning/vagrant_inventory"
    ansible.playbook = "provisioning/main.yml"
    ansible.verbose = "vvv"
    ansible.limit = ["192.168.11.10"]
  end

end
