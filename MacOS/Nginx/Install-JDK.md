# Install JDK on MacOS

`https://www.cnblogs.com/imzhizi/p/macos-jdk-installation-homebrew.html`

```shell script
# 最新版 Oracle JDK
brew cask install oracle-jdk

# Oracle JDK11、Oracle JDK8 需要手动下载
# https://www.oracle.com/hk/java/technologies/javase-downloads.html

# 最新版 Oracle OpenJDK
brew cask install java

# Oracle OpenJDK11
brew cask install java11

# 使用该命令则安装由 Oracle 提供的最新版的 OpenJDK
brew cask install java

# 使用该命令则安装由 Oracle 提供的 OpenJDK11
brew cask install java11

# OpenJDK 在 Oracle 不再维护后会转交给 RedHat 维护
brew cask install openjdk@11

# AdoptOpenJDK 
brew cask install AdoptOpenJDK/openjdk/adoptopenjdk8
brew cask install AdoptOpenJDK/openjdk/adoptopenjdk9
brew cask install AdoptOpenJDK/openjdk/adoptopenjdk10
brew cask install AdoptOpenJDK/openjdk/adoptopenjdk11
brew cask install AdoptOpenJDK/openjdk/adoptopenjdk12
brew cask install AdoptOpenJDK/openjdk/adoptopenjdk

# Azul Zulu 提供了 JDK 7
# Azul Zulu 也提供其他版本的 JDK 像 zulu8、zulu11 等
brew cask install homebrew/cask-versions/zulu7
brew cask install homebrew/cask-versions/zulu8
brew cask install homebrew/cask-versions/zulu11
brew cask install homebrew/cask-versions/zulu

# Apple 提供的 JDK6
brew cask install homebrew/cask-versions/java6
```

Oracle JDK

```shell script
# 运行以下命令会安装最新版本的 Oracle JDK
## 2019-5, 该命令会安装 Oracle JDK 12
## 2020-3, 该命令则会安装 Oracle JDK 13
brew cask install oracle-jdk
```

Oracle OpenJDK

```shell script
# 使用该命令则安装由 Oracle 提供的最新版的 OpenJDK
## 2020-3, 这个命令会安装 OpenJDK13
brew cask install java

# 使用该命令则安装由 Oracle 提供的 OpenJDK11
brew cask install java11

# OpenJDK 在 Oracle 不再维护后会转交给 RedHat 维护
brew cask install openjdk@11
```

AdoptOpenJDK

```shell script
brew cask install AdoptOpenJDK/openjdk/adoptopenjdk8
brew cask install AdoptOpenJDK/openjdk/adoptopenjdk9
brew cask install AdoptOpenJDK/openjdk/adoptopenjdk10
brew cask install AdoptOpenJDK/openjdk/adoptopenjdk11
brew cask install AdoptOpenJDK/openjdk/adoptopenjdk12

# 安装最新版本 OpenJDK
brew cask install AdoptOpenJDK/openjdk/adoptopenjdk
```
