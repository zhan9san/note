[
    {
        "Id": "6074efebc47a73501fa6a12fabeb5c75528335902c8049a777b38cc584d8d03a",
        "Created": "2022-03-15T13:53:59.712022959Z",
        "Path": "/usr/local/bin/entrypoint",
        "Args": [
            "/sbin/init"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 8167,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2022-03-15T13:58:24.688379003Z",
            "FinishedAt": "2022-03-15T13:58:19.630557862Z"
        },
        "Image": "sha256:1312ccd2422d964b2df363d606d0c016d6acbc1ddf0211c26a74717f2897dc43",
        "ResolvConfPath": "/var/lib/docker/containers/6074efebc47a73501fa6a12fabeb5c75528335902c8049a777b38cc584d8d03a/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/6074efebc47a73501fa6a12fabeb5c75528335902c8049a777b38cc584d8d03a/hostname",
        "HostsPath": "/var/lib/docker/containers/6074efebc47a73501fa6a12fabeb5c75528335902c8049a777b38cc584d8d03a/hosts",
        "LogPath": "/var/lib/docker/containers/6074efebc47a73501fa6a12fabeb5c75528335902c8049a777b38cc584d8d03a/6074efebc47a73501fa6a12fabeb5c75528335902c8049a777b38cc584d8d03a-json.log",
        "Name": "/minikube",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "unconfined",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": [
                "/lib/modules:/lib/modules:ro",
                "minikube:/var"
            ],
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "minikube",
            "PortBindings": {
                "22/tcp": [
                    {
                        "HostIp": "127.0.0.1",
                        "HostPort": ""
                    }
                ],
                "2376/tcp": [
                    {
                        "HostIp": "127.0.0.1",
                        "HostPort": ""
                    }
                ],
                "32443/tcp": [
                    {
                        "HostIp": "127.0.0.1",
                        "HostPort": ""
                    }
                ],
                "5000/tcp": [
                    {
                        "HostIp": "127.0.0.1",
                        "HostPort": ""
                    }
                ],
                "8443/tcp": [
                    {
                        "HostIp": "127.0.0.1",
                        "HostPort": ""
                    }
                ]
            },
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "host",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": true,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": [
                "seccomp=unconfined",
                "apparmor=unconfined",
                "label=disable"
            ],
            "Tmpfs": {
                "/run": "",
                "/tmp": ""
            },
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 2000000000,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [
                {
                    "PathOnHost": "/dev/fuse",
                    "PathInContainer": "/dev/fuse",
                    "CgroupPermissions": "rwm"
                }
            ],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "KernelMemory": 0,
            "KernelMemoryTCP": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": null,
            "ReadonlyPaths": null
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/9a7b7154b9d42b2e563db21d58d9d437e56d1e1a88ae046c3788e4be3b65c975-init/diff:/var/lib/docker/overlay2/286b9389386e0ea823fe36f8096dfaea89bb090359659644d10a86404e1f854b/diff:/var/lib/docker/overlay2/7bceb0ea33778eb842e78c3c6df53df4e42aa0cf6c1fd9bdd6bd98ccfcda6d8d/diff:/var/lib/docker/overlay2/9882274d4eb918b11eff3d802165520ce8e821dc1aa2a7ce9e6f2763337d99af/diff:/var/lib/docker/overlay2/278f51caf4444bfab3aadb834a0683537d5007119c5dc84399b37a2a08fb9fa4/diff:/var/lib/docker/overlay2/d7a32d62f28a80cd11d951553cabebeeb3dc1a77af590a307cb279fb84ae2be7/diff:/var/lib/docker/overlay2/87c0e157f820cdea6f34bfe71eee28493ef56b6e9e19344e4c5bb56ab0ff830a/diff:/var/lib/docker/overlay2/73ee9c4dda90afc7294d7db13dacfacafed407de47b6b0228527c11f92b25a45/diff:/var/lib/docker/overlay2/e7086867701cff27c17aaf0b1b05c813fbb9890c760f2ca187771e234987fedc/diff:/var/lib/docker/overlay2/ac04807eaeaf6ad07a385dea8af16209b66ad6b243a2eb12359259d1bcd75c63/diff:/var/lib/docker/overlay2/1b99cff4a7826c2fd4e93ad7e96a56f299003ea8925eb63784ee0a3631c274f6/diff:/var/lib/docker/overlay2/8711446d2f09688ddb725e48074f3d1882f0a7edb8c903e7947ab1c303628a82/diff:/var/lib/docker/overlay2/abb16d85ce05dbd909260d78ee15b0f86852055e3f30937db0621c6ba7df40fb/diff:/var/lib/docker/overlay2/9ecdc39d9ab5f3ac7a73ce43346f89d0eb577538d15e774c07bd950c08eb17e6/diff:/var/lib/docker/overlay2/51e2a47dc200e44e747f33a8ae8e8e945c6d9f104b61e72a4a4883797d74e4dd/diff:/var/lib/docker/overlay2/0d0d9dd399b31de4e119dbd92699e492f0852ed14c915d51e6f806de0ba63ab6/diff:/var/lib/docker/overlay2/cce6d9a14470605c8523191d6d5ff10decfc89269abcff624efc725cb70a3514/diff:/var/lib/docker/overlay2/691eff9de40368ae78d4ac4ad06f96a88f7baebb3a5da2a356600938a5c55ab1/diff:/var/lib/docker/overlay2/3aa921a12eda51c7712eda4577b91a59cab954c669e457b15982aab7bee91d12/diff:/var/lib/docker/overlay2/a19f9384d36461000cdfb09359109e26c754f7e67f193002a3c54949170454ff/diff:/var/lib/docker/overlay2/e5ee29e9bbd2e8f56f6549d56d50eeef4bbe66690802ca362d440f52de9e7d64/diff:/var/lib/docker/overlay2/b09b127dc284d33461b0cb4958fd5fab8aa5b0587f898ebd72d62daca78e6887/diff:/var/lib/docker/overlay2/d0277a9fd4a76497401a3c4cc60f0dcdd3926cbbfc163a2030411198c289173e/diff:/var/lib/docker/overlay2/85a5a7695028279a3e5868f1f22bc08c64d66fc464814d0c1eafcfc6f3d9490c/diff:/var/lib/docker/overlay2/e5dc7a57ff8a5aa0e6bc173c3c5f47859b78cb8a55653cf06b6e72e4b7013c7c/diff:/var/lib/docker/overlay2/4d6c629d2ed10f1e3df183ca5d8e08d21bf36bbc8a4c9063ab6ca5be2f2050ed/diff:/var/lib/docker/overlay2/a40e27dadf16611f8e470b99b55d7e30a35d66e0b832d824f867ad2c22e6e921/diff:/var/lib/docker/overlay2/878808e461adcc3ed6419a746b21c1f5c51fcd77c37661b572fc5f362d759349/diff:/var/lib/docker/overlay2/72e2f82bdae1c4adf1817fccec897be64e4eb79a2bdc37671acb89bc219f2678/diff:/var/lib/docker/overlay2/8dc92a8394aeaf73d6a052b5073cc0093c0305370c3b0a2334ae151a5c17b1c8/diff:/var/lib/docker/overlay2/c6609c77897244efbc5e51b63ac9f9485674ad4f37e6a61c1cd507ef086d4ab6/diff:/var/lib/docker/overlay2/bfbb7dc14ff8924618d320497290445b3cb6db0f92cd1e62340365bb57c892e1/diff:/var/lib/docker/overlay2/9cf8bb1988b5d76f0b7c79ed72e5a06b6ff3024b6a764b5a1030a93f987baab0/diff:/var/lib/docker/overlay2/75b9922980fe9cf8c00ca9c78ad43f98406539e3cf3a64f76da51004f023ca8c/diff:/var/lib/docker/overlay2/ef592eba950012979caaafb2014dececf1ad235aaeb1b7d2bba78513023e7683/diff:/var/lib/docker/overlay2/32b9b816b463fa074eacb95ea9ede86ad8c24704acaebd35f11a05c745436df4/diff:/var/lib/docker/overlay2/97569dcc9a4d39ef9715d7a34963b7b9591e56ae9afdf6175c42ddf3b81cf3bc/diff:/var/lib/docker/overlay2/80e037a86411d73bfafaac7d67a52f68550c2691f548ce95d86b1039b7ac1ab9/diff:/var/lib/docker/overlay2/db82352e41ea052fc5d9d96f1418b827312154e81b6d9d07b10a582dff6b4228/diff:/var/lib/docker/overlay2/10f02c3f6b0fb64adc9ad19b4eab04d2f07add4af388e6308b92373724f5ea15/diff:/var/lib/docker/overlay2/388c534d837e153e2c6c0b0d8a4def5a9cc0e4c136e4126464ae1ac855811240/diff:/var/lib/docker/overlay2/ac6ac1739ebb3be8e6eebb6b8b6dca9cd86777119af56ae2f51496804774700b/diff:/var/lib/docker/overlay2/7d32b5d4c779765674defe325ba98953288306415a4087f6eabfb34ebc1c11ca/diff:/var/lib/docker/overlay2/03ae44eb7cc5255b69045e86d0393577744ffe73a34451ca7c05d73c088e7afe/diff:/var/lib/docker/overlay2/047a57521f4a352de0775cdf15ee5a52f2ee1238176add09978d8d552250505b/diff:/var/lib/docker/overlay2/b06e46d18061eee3e2d84f841eda751f2cd44c3d5423b8afac43e72f179a95a8/diff",
                "MergedDir": "/var/lib/docker/overlay2/9a7b7154b9d42b2e563db21d58d9d437e56d1e1a88ae046c3788e4be3b65c975/merged",
                "UpperDir": "/var/lib/docker/overlay2/9a7b7154b9d42b2e563db21d58d9d437e56d1e1a88ae046c3788e4be3b65c975/diff",
                "WorkDir": "/var/lib/docker/overlay2/9a7b7154b9d42b2e563db21d58d9d437e56d1e1a88ae046c3788e4be3b65c975/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [
            {
                "Type": "bind",
                "Source": "/lib/modules",
                "Destination": "/lib/modules",
                "Mode": "ro",
                "RW": false,
                "Propagation": "rprivate"
            },
            {
                "Type": "volume",
                "Name": "minikube",
                "Source": "/var/lib/docker/volumes/minikube/_data",
                "Destination": "/var",
                "Driver": "local",
                "Mode": "z",
                "RW": true,
                "Propagation": ""
            }
        ],
        "Config": {
            "Hostname": "minikube",
            "Domainname": "",
            "User": "root",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "22/tcp": {},
                "2376/tcp": {},
                "32443/tcp": {},
                "5000/tcp": {},
                "8443/tcp": {}
            },
            "Tty": true,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "container=docker",
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": null,
            "Image": "registry.cn-hangzhou.aliyuncs.com/google_containers/kicbase:v0.0.30",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": [
                "/usr/local/bin/entrypoint",
                "/sbin/init"
            ],
            "OnBuild": null,
            "Labels": {
                "created_by.minikube.sigs.k8s.io": "true",
                "mode.minikube.sigs.k8s.io": "minikube",
                "name.minikube.sigs.k8s.io": "minikube",
                "role.minikube.sigs.k8s.io": ""
            },
            "StopSignal": "SIGRTMIN+3"
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "aba520194c14e5bfa9ff39d9fd698c3eb6b91d0365f52b0b9523b9fb9e2f9caa",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {
                "22/tcp": [
                    {
                        "HostIp": "127.0.0.1",
                        "HostPort": "49162"
                    }
                ],
                "2376/tcp": [
                    {
                        "HostIp": "127.0.0.1",
                        "HostPort": "49161"
                    }
                ],
                "32443/tcp": [
                    {
                        "HostIp": "127.0.0.1",
                        "HostPort": "49158"
                    }
                ],
                "5000/tcp": [
                    {
                        "HostIp": "127.0.0.1",
                        "HostPort": "49160"
                    }
                ],
                "8443/tcp": [
                    {
                        "HostIp": "127.0.0.1",
                        "HostPort": "49159"
                    }
                ]
            },
            "SandboxKey": "/var/run/docker/netns/aba520194c14",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "",
            "Gateway": "",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "",
            "IPPrefixLen": 0,
            "IPv6Gateway": "",
            "MacAddress": "",
            "Networks": {
                "minikube": {
                    "IPAMConfig": {
                        "IPv4Address": "192.168.49.2"
                    },
                    "Links": null,
                    "Aliases": [
                        "6074efebc47a",
                        "minikube"
                    ],
                    "NetworkID": "84371233d732516f78471b9f84a7823a496b12156327aa1ff35313f58e3cc0c6",
                    "EndpointID": "750d143e72111fa2edfc7b98ad732d00f79d78eeb7bb49981b64a14506ee58cd",
                    "Gateway": "192.168.49.1",
                    "IPAddress": "192.168.49.2",
                    "IPPrefixLen": 24,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:c0:a8:31:02",
                    "DriverOpts": null
                }
            }
        }
    }
]
