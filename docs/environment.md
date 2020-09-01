# Linux setup

## Install nvm

[https://github.com/nvm-sh/nvm#installation-and-update](https://github.com/nvm-sh/nvm#installation-and-update)

- `nvm install 12`
- `nvm use 12`
- `nvm install-latest-npm`

## Install git

- `sudo apt-get install libsecret-1-0 libsecret-1-dev`
- `cd /usr/share/doc/git/contrib/credential/libsecret`
- `sudo make`
- `git config --global credential.helper /usr/share/doc/git/contrib/credential/libsecret/git-credential-libsecret`
- `git clone https://gitlab.takiwa.co/root/takiwa-product.git`

## Increase max watchers
`echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p`

## Install docker
- `sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -`
- `sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"`
- `sudo apt update`
- `sudo apt install docker-ce`


## Install mongo
- `sudo docker pull mongo`
- `mkdir takiwa-mongo`
- `sudo docker run --name takiwa-mongo -v ~/takiwa-mongo:/data/db -p 27017:27017 -d mongo:4.0-xenial`
- `sudo docker start takiwa-mongo`