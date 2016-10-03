Vagrant.configure("2") do |config|

    config.vm.box = "ubuntu/trusty64"

    config.vm.hostname = "vagrant-lamp-dev"
    config.vm.network :private_network, ip: "192.168.4.10"
    config.hostsupdater.aliases = ["dev.vagrant-my.fr"]
    config.hostsupdater.remove_on_suspend = true


    config.vm.synced_folder "web/", "/vagrant", id: "vagrant-root"


    config.vm.provision :puppet do |puppet|
        puppet.manifests_path = "puppet/manifests"
        puppet.module_path = "puppet/modules"
        puppet.options="--verbose --debug"
    end

    # Fix for slow external network connections
    config.vm.provider :virtualbox do |vb|
        vb.memory = 2048
        vb.customize ['modifyvm', :id, '--natdnshostresolver1', 'on']
        vb.customize ['modifyvm', :id, '--natdnsproxy1', 'on']
    end
end