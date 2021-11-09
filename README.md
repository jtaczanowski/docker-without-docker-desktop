# docker-without-docker-desktop
Use docker without docker dekstop.

Instead of using docker dekstop use your own docker daemon on locally runing Virtual Machine (Vagrant on Virtualbox).

## How to use
## macOS
#### Required software
- Install Virtualbox https://www.virtualbox.org/wiki/Downloads
- Install Vagrant https://www.vagrantup.com/downloads
- Install Homebrew https://brew.sh/
- Install docker client:
```brew install docker``` 

#### Start remote docker daemon (virtual machine on your Vagrant)
- In project directory run ```vagrant up```

#### Configure docker client on your machine to use remote docker daemon
```docker context create remote --docker host=tcp://localhost:2375```

```docker context use remote```

#### Test your newly configured environment
```docker run hello-world```
