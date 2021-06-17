# Introduction

Groups can hold many organizations, and each organization can contain many collaborators.

As well as creating organizations within your enterprise groups, you can also create them within your own personal group. This is ideal if you want to monitor your own personal projects outside of your enterprise’s group, or if you want a sandbox to play with.

1. No group concept for Sync container
2. The image with different tags will be considered as one Snyk project.
   `jenkins/inbound-agent:latest` and `jenkins/inbound-agent:4.3-4` will in
   project `docker-image|jenkins/inbound-agent`.

```bash
snyk container test ubuntu:18.04 --org=my-team
snyk container test app:latest --file=Dockerfile --policy-path=path/to/.snyk


snyk container test --exclude-base-image-vulns --file=11/debian/Dockerfile jenkins/inbound-agent:4.3-3

```
