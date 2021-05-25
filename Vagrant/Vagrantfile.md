# Vagrantfile

```bash
$ cat Vagrantfile | grep -vE "^\s*#|^\s*$"
Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.network "public_network", bridge: "en0: Wi-Fi (AirPort)"
  config.vm.provider "virtualbox" do |vb|
      vb.memory = "4096"
      vb.cpus = 2
  end
end
```

Ubuntu: `bento/ubuntu-20.04`
