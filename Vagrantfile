Vagrant.configure("2") do |config|
  config.vm.box = "bento/centos-8.1"
  config.vm.network "private_network", ip: "192.168.64.30"
  config.vm.hostname = "dama"
  config.vm.provision "shell", inline: <<-SHELL
    su - vagrant
    wget -q https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O miniconda.sh
    chmod +x miniconda.sh
    ./miniconda.sh -b -p /home/vagrant/miniconda
    echo 'export PATH="/home/vagrant/miniconda/bin:$PATH"' >> /home/vagrant/.bashrc
    source /home/vagrant/.bashrc
    chown -R vagrant:vagrant /home/vagrant/miniconda
    /home/vagrant/miniconda/bin/conda install conda-build anaconda-client conda-pack -y -q
    /home/vagrant/miniconda/condabin/conda init bash
  SHELL
  config.vm.provision "file", source: "~/.ssh", destination: "$HOME/.ssh"
  config.vm.provision "file", source: "~/.vimrc", destination: "$HOME/.vimrc"
  config.vm.provision "file", source: "~/.gitconfig", destination: ".gitconfig"
  config.vm.provision "file", source: "collection-2020-2.0rc8.tar.gz", destination: "collection-2020-2.0rc8.tar.gz"
  config.vm.synced_folder "~/", "/home/vagrant/host_home"
  config.vm.provision "shell", inline: <<-SHELL
    mkdir /home/vagrant/miniconda/envs/collection-2020-2.0rc8
    tar -xvzf collection-2020-2.0rc8.tar.gz -C /home/vagrant/miniconda/envs/collection-2020-2.0rc8/
    su - vagrant
    source activate /home/vagrant/miniconda/envs/collection-2020-2.0rc8/
    conda-unpack
  SHELL
end
