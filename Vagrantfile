Vagrant.configure("2") do |config|
  config.vm.box = "bento/centos-8"
  config.vbguest.auto_update = true

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.164.164"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "zookeeper-playbook.yml"
    ansible.extra_vars = {}
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "kafka-playbook.yml"
    ansible.extra_vars = {
      broker_id: "10",
      zookeeper_connect: "localhost:2181"
    }
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "bluesky-playbook.yml"
    ansible.extra_vars = {
      zookeeper: "localhost:2181",
      bluesky_topic: "bluesky-kafka-test",
      bluesky_topic_replication_factor: 1,
      bluesky_topic_partitions: 1
    }
  end

end
