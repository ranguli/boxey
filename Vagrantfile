Vagrant.configure("2") do |config|

    config.vm.box = "ubuntu/xenial64"
    config.vm.hostname = "boxey"
   
    # Tell Vagrant not to insert its own SSH key. 
    config.ssh.insert_key = false 

    # Copy over the host private key in order to push to git
    config.vm.provision "file", source: "~/.ssh/id_rsa", destination: "~/.ssh/id_rsa"

    # Provision the Vagrant box with Ansible. 
    config.vm.provision "ansible_local" do |ansible|
        ansible.verbose = "v"
        ansible.playbook = "playbook.yml"
    end
end
