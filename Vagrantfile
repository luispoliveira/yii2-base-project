Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/xenial64"
    config.vm.network :forwarded_port, guest: 80, host: 8080, auto_correct: true
    config.vm.network :private_network, ip: '192.168.2.101'
    config.vm.provision :ansible_local do |ansible|
        ansible.playbook = "provisioning/bootstrap.yml"
    end

    host = RbConfig::CONFIG['host_os']
    if host =~ /darwin/
        config.vm.synced_folder '.', '/vagrant', nfs: true, mount_options: ['rw', 'vers=3', 'tcp', 'fsc', 'noatime', 'nodiratime']
    elsif host =~ /linux/
    	config.vm.synced_folder '.', '/vagrant', nfs: true, mount_options: ['nolock', 'vers=3,udp', 'noatime']
    else
     	config.vm.synced_folder ".", "/vagrant"
    end

    config.vm.provider "virtualbox" do |vb|
        vb.memory = "4096"
    end
end