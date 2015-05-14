Vagrant.configure(2) do |config|
  config.vm.box = "trusty"
  config.vm.box_url = "http://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"
  config.vm.network "private_network", ip: "192.168.0.37"
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y git python-dev
    curl -# https://bootstrap.pypa.io/get-pip.py|sudo python
    pip install --user --upgrade git+git://github.com/signalfuse/maestro-ng
    wget -qO- https://get.docker.com/ | sh
    echo -e "`cat /etc/default/docker`\n\nDOCKER_OPTS=\\"-H tcp://192.168.0.37:4243\\""|sudo tee /etc/default/docker
    sudo service docker restart
    python -m maestro -f /vagrant/maestro.yml start
  SHELL
end
