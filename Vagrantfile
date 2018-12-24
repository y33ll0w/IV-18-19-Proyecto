Vagrant.configure("2") do |config|

    config.vm.define :machine_google do |machine_google|
        config.vm.box = "google/gce"
        config.vm.network "private_network", guest: 80, host: 80

        machine_google.vm.provider :google do |google, override|
            google.google_project_id = ENV['PROJECT_ID']
            google.google_client_email = ENV['CLIENT_EMAIL']
            google.google_json_key_location = ENV['JSON_PRIV_KEY']
            
            google.image_family = 'ubuntu-1604-lts'
            google.name = 'cloudncloud'
            google.machine_type = 'g1-small'

            override.ssh.username = "djskullz8"
            override.ssh.private_key_path = "~/.ssh/my-ssh-key"
        end
    end

    config.vm.define :machine_azure do |machine_azure|
        config.vm.box = 'azure'
        config.vm.network "private_network", guest: 80, host: 80

        machine_azure.vm.provider :azure do |azure, override|
            azure.tenant_id = ENV['AZURE_TENANT_ID']
            azure.client_id = ENV['AZURE_CLIENT_ID']
            azure.client_secret = ENV['AZURE_CLIENT_SECRET']
            azure.subscription_id = ENV['AZURE_SUBSCRIPTION_ID']

            azure.vm_size = 'Standard_B1ms'
            azure.location = 'westeurope'
		    azure.vm_name = 'cloudncloud'
            azure.resource_group_name= 'cloudncloudgroup'
		    azure.tcp_endpoints = '80'

            override.vm.synced_folder ".", "/vagrant", disabled: true
            override.ssh.username = "djskullz8"
            override.ssh.private_key_path = "~/.ssh/my-ssh-key"
        end
    end

    config.vm.provision :ansible do |ansible|
        ansible.playbook = "provision/playbook.yml"
    end
end