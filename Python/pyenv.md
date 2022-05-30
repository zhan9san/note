# Install pyenv

<https://github.com/pyenv/pyenv#automatic-installer>

```shell
$ cat Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-20.04"
  config.vm.network "public_network", bridge: "enp0s31f6"
end
```

```shell
sudo apt-get install --yes git
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```

Ubuntu

```shell
sudo apt-get update; sudo apt-get install make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev -y
```
