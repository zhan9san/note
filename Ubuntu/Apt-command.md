# apt-get

* list all installed packages

```bash
apt list --installed
```

* upgrade or update a single package using apt-get
  * Fetch package index by running `sudo apt update` command
  * Only update apache2 package by running `sudo apt install apache2` command
  * If apache2 package already installed it will try to update to the latest
  version. If you do not want to install new packages; when used in conjunction
  with install, only-upgrade will install upgrades for already installed
  packages only and ignore requests to install new packages. Try
  `sudo apt --only-upgrade install apache2`

* see availble updates
  `apt list --upgradable`

## How To Exclude Packages from Apt-Get Upgrade

`https://tecadmin.net/exclude-packages-from-apt-upgrade/`

* Hold or Exclude Packages from Upgrade
  `sudo apt-mark hold package_name`

* List Packages on Hold
  `sudo dpkg --get-selections | grep "hold"`

* Unhold or Enable Package Upgrade
  `sudo apt-mark unhold package_name`

* update all packages
  `sudo apt upgrade -y`

In most of the cases after updating, there are some packages the are of no further use to the user. You can delete them, which will free up your system space and keep your system clean and tidy, which is always a good thing.

`sudo apt autoremove`