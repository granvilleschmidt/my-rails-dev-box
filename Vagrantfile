Vagrant.configure("2") do |config|
  config.vm.box       = 'precise64'
  config.vm.box_url   = 'http://files.vagrantup.com/precise64.box'
  config.vm.host_name = 'my-rails-dev-box'

  config.vm.network :forwarded_port, guest: 3000, host: 3000
  config.vm.network :forwarded_port, guest: 4567, host: 4567

  # MailCatcher default HTTP port.
  config.vm.network :forwarded_port, guest: 1080, host: 1080

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end

  config.vm.provision :puppet do |puppet|
    puppet.manifests_path = 'puppet/manifests'
    puppet.module_path    = 'puppet/modules'
    puppet.manifest_file  = 'default.pp'
    puppet.options = "--verbose --debug"
  end

  config.vm.provision :shell, path: './provision.sh'
end
