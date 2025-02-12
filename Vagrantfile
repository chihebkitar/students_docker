

Vagrant.configure("2") do |config|
  config.vm.define "docker" do |docker|
    # CHANGED: Use official Ubuntu 20.04 box
    docker.vm.box = "ubuntu/focal64"
    docker.vm.network "private_network", type: "static", ip: "192.168.56.5"
    docker.vm.hostname = "docker"
    docker.vm.provider "virtualbox" do |v|
      v.name = "docker"
      v.memory = 6144
      v.cpus = 2
    end
    docker.vm.provision :shell do |shell|
      shell.path = "install_docker.sh"
      shell.env = { 'ENABLE_ZSH' => ENV['ENABLE_ZSH'] }
    end
  end
end