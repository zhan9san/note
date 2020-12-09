# Proxy

```shell script
$ brew install polipo
To have launchd start polipo now and restart at login:
  brew services start polipo
Or, if you don't want/need a background service you can just run:
  polipo
==> Summary
🍺  /usr/local/Cellar/polipo/1.1.1: 74 files, 613.8KB
Warning: Calling depends_on :java is deprecated! Use "depends_on "openjdk@11", "depends_on "openjdk@8" or "depends_on "openjdk" instead.
Please report this issue to the homebrew/core tap (not Homebrew/brew or Homebrew/core), or even better, submit a PR to fix it:
  /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core/Formula/libbluray.rb:23
```

Config

```shell script
❯ cat ~/.polipo                                                                                                      17:14:44
socksParentProxy = "127.0.0.1:50000"
socksProxyType = socks5
allowedClients = "0.0.0.0/0"
proxyAddress = "0.0.0.0"
proxyPort = 8123
```

Reference:  
`https://stackoverflow.com/questions/34749303/missing-polipo-config-file-in-usr-local-etc`

Get config from `http://127.0.0.1:8123/polipo/config`
