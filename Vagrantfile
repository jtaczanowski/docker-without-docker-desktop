# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.vm.box = "opensuse/Leap-15.3.x86_64"
    config.vm.network "forwarded_port", guest: 2375, host: 2375
    config.vm.provision "shell", inline: <<-SHELL
      zypper --non-interactive addrepo https://download.opensuse.org/repositories/Virtualization:/containers/openSUSE_Leap_15.3/ containters
      zypper --gpg-auto-import-keys refresh
      zypper --non-interactive update
      zypper --non-interactive install docker
    
      usermod -G docker -a vagrant
  
      echo \
      '{
        \"log-level\": \"warn\",
        \"log-driver\": \"json-file\",
        \"log-opts\": {
          \"max-size\": \"10m\",
          \"max-file\": \"5\"
        },
        \"hosts\": [\"tcp://0.0.0.0:2375\", \"unix:///var/run/docker.sock\"]}' | tee /etc/docker/daemon.json > /dev/null
      systemctl enable docker
      systemctl start docker
      systemctl status docker
      printf "\n\nNow on your local machine you can configure docker client to use docker daemon installed on this VM\ndocker context create remote --docker "host=tcp://localhost:2375"\ndocker context use remote\n\n"
    SHELL
  end
  