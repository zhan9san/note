# Installation

```bash
curl -o jfrog-artifactory-pro-rpms.repo https://releases.jfrog.io/artifactory/artifactory-pro-rpms/artifactory-pro-rpms.repo;
sudo mv jfrog-artifactory-pro-rpms.repo /etc/yum.repos.d/;
sudo yum update -y && sudo yum install -y jfrog-artifactory-pro-6.17.0;
```
