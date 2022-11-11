Vagrant.configure("2") do |db|
  db.vm.define 'mongodb' do |mongodb|
    mongodb.vm.box = 'spox/ubuntu-arm'
    mongodb.vm.network 'private_network',ip: '192.168.56.20'
    mongodb.vm.provider 'vmware_fusion' do |vb|
      #first argument is local and second argument is where it should be on Vm
      mongodb.vm.synced_folder 'env/','/home/vagrant/env'
    vb.gui = true
    end
    mongodb.vm.provision "ansible" do |ansible|
      ansible.verbose = "v"
      ansible.playbook = "env/mongodb/playbook.yml"
    end
  end
end

Vagrant.configure("2") do |config|
    config.vm.define "nodeapp" do |nodeapp|
      nodeapp.vm.box = "spox/ubuntu-arm"
      nodeapp.vm.network "private_network", ip: "192.168.56.10"
      nodeapp.hostsupdater.aliases = ["nology.training"]
      nodeapp.vm.provider "vmware_fusion" do |vb|
        nodeapp.vm.synced_folder "app/", "/home/vagrant/app/"
        nodeapp.vm.synced_folder "env/", "/home/vagrant/env"
        vb.gui = true
      end
      nodeapp.vm.provision "ansible" do |ansible|
        ansible.verbose = "v"
        ansible.playbook = "env/nodeapp/playbook.yml"
      end
    end
end