# Atlassian SDK

## Install the Atlassian SDK on Ubuntu

1. Configure your environment

    ```bash
    echo 'export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64' >> ~/.bashrc
    echo 'export PATH=$PATH:$JAVA_HOME/bin' >> ~/.bashrc
    ```

2. Download and install the SDK

    ```bash
    sudo sh -c 'echo "deb https://packages.atlassian.com/debian/atlassian-sdk-deb/ stable contrib" >>/etc/apt/sources.list'
    wget https://packages.atlassian.com/api/gpg/key/public    
    sudo apt-key add public   
    sudo apt-get update
    sudo apt-get install atlassian-plugin-sdk
    ```

3. Verify that you have set up the SDK correctly

    ```bash
    $ atlas-version

    ATLAS Version:    8.2.8
    ATLAS Home:       /usr/share/atlassian-plugin-sdk-8.2.8
    ATLAS Scripts:    /usr/share/atlassian-plugin-sdk-8.2.8/bin
    ATLAS Maven Home: /usr/share/atlassian-plugin-sdk-8.2.8/apache-maven-3.5.4
    AMPS Version:     8.1.2
    --------
    Executing: /usr/share/atlassian-plugin-sdk-8.2.8/apache-maven-3.5.4/bin/mvn --version -gs /usr/share/atlassian-plugin-sdk-8.2.8/apache-maven-3.5.4/conf/settings.xml
    Apache Maven 3.5.4 (1edded0938998edf8bf061f1ceb3cfdeccf443fe; 2018-06-18T02:33:14+08:00)
    Maven home: /usr/share/atlassian-plugin-sdk-8.2.8/apache-maven-3.5.4
    Java version: 1.8.0_292, vendor: Private Build, runtime: /usr/lib/jvm/java-8-openjdk-amd64/jre
    Default locale: en, platform encoding: UTF-8
    OS name: "linux", version: "5.4.0-74-generic", arch: "amd64", family: "unix"
    ```
