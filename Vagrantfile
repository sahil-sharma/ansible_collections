# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/jammy64"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = 2048
    vb.cpus = 1
  end

  config.vm.define "ansible" do |ansible|
      ansible.vm.hostname = "ansible"
      ansible.vm.network "private_network", ip: "192.168.56.30"
      ansible.vm.network "public_network", bridge: "wlp0s20f3"
      ansible.vm.provision "shell", inline: 'sudo apt-add-repository ppa:ansible/ansible --yes \
        && sudo apt install tree ansible -y \
        && cp /vagrant/id_rsa* /home/vagrant/.ssh \
        && echo "export ANSIBLE_COLLECTION_PATH=/vagrant/test/my_collection" >> /home/vagrant/.bashrc \
        && source /home/vagrant/.bashrc'
  end

  config.vm.define "test1" do |test1|
      test1.vm.hostname = "test1"
      test1.vm.network "private_network", ip: "192.168.56.31"
      test1.vm.network "public_network", bridge: "wlp0s20f3"
      test1.vm.provision "shell", inline: 'echo "Host 192.168.56.*" >> /home/vagrant/.ssh/config \
        && echo -e "  StrictHostKeyChecking no\n" >> /home/vagrant/.ssh/config \
        && echo -e "  User vagrant" >> /home/vagrant/.ssh/config \
        && cat /vagrant/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys \
        && sudo chown vagrant:vagrant /home/vagrant/.ssh/config \
        && sudo chmod 0700 /home/vagrant/.ssh/config'
  end
end
