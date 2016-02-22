BOX = "ubuntu/trusty64"
HOSTNAME = "pomodoro.dev"
MEMORY = 1024
CPUS = 2
IP = "192.168.11.10"
INVENTORY = "vagrant_inventory"
PLAYBOOK  = "main.yml"

Vagrant.configure('2') do |config|
  config.vm.box = BOX
  config.vm.hostname = HOSTNAME
  config.ssh.shell = "bash -c \'BASH_ENV=/etc/profile exec bash\'"

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--memory", MEMORY]
    vb.customize ["modifyvm", :id, "--cpus", CPUS]
  end

  config.vm.network :private_network, ip: IP
  config.vm.network "forwarded_port", guest: 80, host: 8080

  config.vm.synced_folder "./", "/main", type: "nfs", :mount_options => ['nolock,vers=3,udp,noatime,actimeo=1']

  config.vm.provision :ansible do |ansible|
    ansible.inventory_path = "provisioning/#{INVENTORY}"
    ansible.playbook = "provisioning/#{PLAYBOOK}"
    ansible.verbose = "vvv"
    ansible.limit = [IP]
  end

end
