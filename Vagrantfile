Vagrant.configure("2") do |config|
  servers=[
    {
      :hostname => "lamp-server01",
      :box => "bento/ubuntu-18.04",
      :ip => "192.168.56.100",
      :ssh_port => '2215'
    },
    {
      :hostname => "docker-server",
      :box => "bento/ubuntu-18.04",
      :ip => "192.168.56.101",
      :ssh_port => '2210'
    },
  ]

  servers.each do |machine|

    config.vm.define machine[:hostname] do |node|
      node.vm.box = machine[:box]
      node.vm.hostname = machine[:hostname]
    
      node.vm.network :private_network, ip: machine[:ip]
      node.vm.network "forwarded_port", guest: 22, host: machine[:ssh_port], id: "ssh"

      node.vm.provider :virtualbox do |v|
        v.customize ["modifyvm", :id, "--memory", 512]
        v.customize ["modifyvm", :id, "--name", machine[:hostname]]
      end
    config.vm.provision "puppet" do |puppet|
      puppet.manifests_path = "manifests"
      puppet.manifest_file = "default.pp"
      end
    end
  end
end