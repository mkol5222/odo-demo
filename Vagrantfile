# based on https://www.itwonderlab.com/en/ansible-kubernetes-vagrant-tutorial/

IMAGE_NAME = "ubuntu/focal64"
CONTROL_NUM = 1
CONTROL_CPU = 2
CONTROL_MEM = 1024


IP_BASE = "192.168.51."

VAGRANT_DISABLE_VBOXSYMLINKCREATE=1

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false

    (1..CONTROL_NUM).each do |i|
        config.vm.define "demo-vm-#{i}" do |master|
            master.vm.network :forwarded_port, guest: 22, host: 2322, id: "ssh"
            master.vm.synced_folder ".", "/vagrant", type: "virtualbox"
            master.vm.box = IMAGE_NAME
            master.vm.network "private_network", ip: "#{IP_BASE}#{i + 10}"
            master.vm.hostname = "demo-vm-#{i}"
            master.vm.provider "virtualbox" do |v|
                v.memory = CONTROL_MEM
                v.cpus = CONTROL_CPU
                v.customize ["modifyvm", :id, "--ioapic", "on"]
            end
            master.vm.provision "shell", inline: <<-SHELL
                apt-get update
                apt-get install -y jq curl python3-pip docker.io docker-compose
                usermod -aG docker vagrant
                cd /vagrant
                sudo docker-compose up -d
            SHELL
        end
    end
end