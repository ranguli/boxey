Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/bionic64"
    config.vm.hostname = "boxey"

    # Because this is a local development machine that does is only accessible
    # locally on the machine it is running from, forwarding ports liberally
    # is for the time being an acceptable security risk. 

    config.vm.network "forwarded_port", guest: 3333, host: 3333, host_ip: "127.0.0.1"
    config.vm.network "forwarded_port", guest: 443, host: 4430, host_ip: "127.0.0.1"
    config.vm.network "forwarded_port", guest: 8080, host: 8080, host_ip: "127.0.0.1"

    config.vm.provider "virtualbox" do |v|
      v.memory = 6000
    end
  
    # Share my projects directory with the VM
    config.vm.synced_folder "../", "/home/vagrant/projects"
    config.vm.synced_folder "../../dotfiles", "/home/vagrant/dotfiles"
    config.vm.synced_folder "./", "/boxey"
 
    # Tell Vagrant not to insert its own SSH key. 
    config.ssh.insert_key = false 

    # Copy over the host private key in order to push to git
    config.vm.provision "file", source: "~/.ssh/id_rsa", destination: "~/.ssh/id_rsa"

    # Provision the Vagrant box with Ansible. 
    config.vm.provision "ansible_local" do |ansible|
        #ansible.verbose = "v"
        ansible.playbook = "/boxey/provisioning/playbook.yml"
    end
end
