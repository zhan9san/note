# Setting up a Windows Host

<https://docs.ansible.com/ansible/latest/user_guide/windows_setup.html#setting-up-a-windows-host>

## Windows SSH Setup

<https://docs.chocolatey.org/en-us/choco/setup#install-with-cmd.exe>

### On target Windows host

#### Install `chocolatey`

```cmd
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "[System.Net.ServicePointManager]::SecurityProtocol = 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```

#### Install `openssh` server

```cmd
choco install --package-parameters=/SSHServerFeature -y openssh
```

### SSH public key authentication

On Ansible host

Upload public key to target host

```shell
scp ~/.ssh/id_rsa.pub username@target_hostname:C:/ProgramData/ssh/administrators_authorized_keys
```

Grant permission of public keys

```shell
ssh username@target_hostname 'icacls C:\ProgramData\ssh\administrators_authorized_keys /inheritance:r /grant "Administrators:F" /grant "SYSTEM:F"'
```

Inventory file

```yml
---
all:
  hosts:
    foo.example.com:
      ansible_user: username
      ansible_shell_type: cmd
      timeout: 120
```

### Verify connection

```shell
$ ansible -i inventory.yml foo.example.com -m ansible.windows.win_ping
foo.example.com | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```
