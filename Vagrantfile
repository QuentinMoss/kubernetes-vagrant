
Vagrant.configure(2) do |config|

  # Start kubernetes master VM configuration
  config.vm.define "kub-master", autostart: true, primary: true do |master|
    master.vm.box = "bento/centos-7.2"

    # set the hostname
    master.vm.hostname = "kub-master"

    # Configuration private networking
    master.vm.network "private_network", ip: '10.127.127.10'
    # Configure port forwarding - visit port 8080 to use port 80 on VM
    master.vm.network "forwarded_port", guest: 80, host: 8080

    # Set memory on VM - minion
    master.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--memory", "1024"]
    end

    # Run ansible playbook
    master.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible/kub-master.yml"
    end
  end
  # End master VM configuration

  # Start kubernetes minion VM configuration
  config.vm.define "kub-minion", autostart: false, primary: false do |minion|
    minion.vm.box = "bento/centos-7.2"

    # Set minion hostname
    minion.vm.hostname = "kub-minion"

    # Configuration private networking
    minion.vm.network "private_network", ip: '10.127.127.11'
    # Configure port forwarding - visit port 8081 to use port 81 on VM
    minion.vm.network "forwarded_port", guest: 81, host: 8081

    # Set memory on VM - minion
    minion.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--memory", "1024"]
    end
    # Run ansible playbook
    minion.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible/kub-minion.yml"
    end
    # End kubernetes VM configuration
  end
end
