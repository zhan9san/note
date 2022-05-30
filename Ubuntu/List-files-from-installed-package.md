# How do I get a list of installed files from a package?

<https://askubuntu.com/questions/32507/how-do-i-get-a-list-of-installed-files-from-a-package>

To see all the files the package installed onto your system, do this:

```shell
dpkg-query -L <package_name>
```

To see the files a .deb file will install

```shell
dpkg-deb -c <package_name.deb>
```
