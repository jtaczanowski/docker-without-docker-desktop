# docker-without-docker-desktop
Use docker without docker desktop.

Instead of using docker desktop use your own docker daemon running on local Virtual Machine (Vagrant on Virtualbox).

## How to use
### macOS
#### Required software
- Install Virtualbox https://www.virtualbox.org/wiki/Downloads
- Install Vagrant https://www.vagrantup.com/downloads
- Install Homebrew https://brew.sh/
- Install docker client:
```brew install docker``` 

#### Start remote docker daemon (virtual machine on your Vagrant)
- In project directory run ```vagrant up```

#### Configure docker client on your machine to use remote docker daemon
```
docker context create remote --docker host=tcp://localhost:2375
```

```
docker context use remote
```

#### Test your newly configured environment
```
docker run hello-world
```
#### Install docker-compose (optionally)
```
sudo curl -L "https://github.com/docker/compose/releases/download/v2.2.3/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

## Troubleshooting
### macOS
#### Problem with logging to remote docker registry.
If you are experiencing error:

```
Error saving credentials: error storing credentials - err: exec: "docker-credential-osxkeychain": executable file not found in $PATH, out:
```

then remove
line with ```credsStore``` key from ~/.docker/config.json
