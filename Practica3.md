# Actividad3:

## **Objetivo**
Desplegar una aplicación en Apache Tomcat.

Se comprueba que el contenedor docker esta corriendo

```code/bash/textplan/console  
 sudo docker ps
CONTAINER ID   IMAGE     COMMAND             CREATED         STATUS         PORTS                                       NAMES
cbbf295cbe21   tomcat    "catalina.sh run"   9 seconds ago   Up 8 seconds   0.0.0.0:9090->8080/tcp, :::9090->8080/tcp   tomcat-server
```

## **Paso 1: se prueba con una aplicación de ejemplo**
```code/bash/textplan/console  
sudo docker cp /home/alumno/Escritorio/sample.war tomcat-server:/usr/local/tomcat/webapps/
Successfully copied 6.66kB to tomcat-server:/usr/local/tomcat/webapps/
```



### Verificar logs

```code/bash/textplan/console  
sudo docker logs tomcat-server
27-Nov-2024 19:43:33.312 INFO [Catalina-utility-2] org.apache.catalina.startup.HostConfig.deployWAR Deployment of web application archive [/usr/local/tomcat/webapps/sample.war] has finished in [800] ms
```

### Utilizar docker inspect

```code/bash/textplan/console  
sudo docker inspect tomcat-server
[
    {
        "Id": "cbbf295cbe21a1490107c39d382b198a4b293c97c72412cf67a8c7e96178dcf5",
        "Created": "2024-11-27T19:40:20.218812607Z",
        "Path": "catalina.sh",
        "Args": [
            "run"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 7009,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2024-11-27T19:40:20.492703492Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:f77539e7e45f7c6337c681589fe18ee6407640e4066c450fcfb8c6a4ba5575b2",
        "ResolvConfPath": "/var/lib/docker/containers/cbbf295cbe21a1490107c39d382b198a4b293c97c72412cf67a8c7e96178dcf5/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/cbbf295cbe21a1490107c39d382b198a4b293c97c72412cf67a8c7e96178dcf5/hostname",
        "HostsPath": "/var/lib/docker/containers/cbbf295cbe21a1490107c39d382b198a4b293c97c72412cf67a8c7e96178dcf5/hosts",
        "LogPath": "/var/lib/docker/containers/cbbf295cbe21a1490107c39d382b198a4b293c97c72412cf67a8c7e96178dcf5/cbbf295cbe21a1490107c39d382b198a4b293c97c72412cf67a8c7e96178dcf5-json.log",
        "Name": "/tomcat-server",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "docker-default",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {
                "8080/tcp": [
                    {
                        "HostIp": "",
                        "HostPort": "9090"
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
            "ConsoleSize": [
                24,
                80
            ],
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
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": [],
            "BlkioDeviceWriteBps": [],
            "BlkioDeviceReadIOps": [],
            "BlkioDeviceWriteIOps": [],
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
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
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware",
                "/sys/devices/virtual/powercap"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/636c3f962a8ce9998996d1e2870dd71b4d802206824eb5916a8c1015a974040b-init/diff:/var/lib/docker/overlay2/350e4c11e67c4d08c7dfa5d1042ab95e0cea4da48d4435e0981e7f533809571f/diff:/var/lib/docker/overlay2/f9983b824d70e8cdab1d9a4abaa9f623864ee256237106b74031275c92e7f1a6/diff:/var/lib/docker/overlay2/a955885ff6a4a00f49029840db0deb7afd3d2bb85e209fb1d7e0355c89adbec9/diff:/var/lib/docker/overlay2/cc14822f1d3377f5ad311563fa0ebe787c93a16138e4936699cadc0d0b5d4d36/diff:/var/lib/docker/overlay2/36628741628ca9fde4fb18eeafa168ac72f08a1a9743efffb80a3c7a8b8234c4/diff:/var/lib/docker/overlay2/e2895e6a8ae4a7335c00866ec34e8378ee6885faa28751e91ffc9048e9ba5fe6/diff:/var/lib/docker/overlay2/1e4fbcfe2ba75f2fd8e96caf24bd6220da0839884c168005f6f8c88cd7ad486f/diff:/var/lib/docker/overlay2/3fc90e6ec21e6cedcef52478a0fef2b2b7a7a87c50b7b29cb745ee2eba2a4176/diff:/var/lib/docker/overlay2/9a38602292aac7942a015cdb2532d60de1316b2cd388a0ca4ac525141d43d933/diff",
                "MergedDir": "/var/lib/docker/overlay2/636c3f962a8ce9998996d1e2870dd71b4d802206824eb5916a8c1015a974040b/merged",
                "UpperDir": "/var/lib/docker/overlay2/636c3f962a8ce9998996d1e2870dd71b4d802206824eb5916a8c1015a974040b/diff",
                "WorkDir": "/var/lib/docker/overlay2/636c3f962a8ce9998996d1e2870dd71b4d802206824eb5916a8c1015a974040b/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "cbbf295cbe21",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "8080/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/tomcat/bin:/opt/java/openjdk/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "JAVA_HOME=/opt/java/openjdk",
                "LANG=en_US.UTF-8",
                "LANGUAGE=en_US:en",
                "LC_ALL=en_US.UTF-8",
                "JAVA_VERSION=jdk-21.0.5+11",
                "CATALINA_HOME=/usr/local/tomcat",
                "TOMCAT_NATIVE_LIBDIR=/usr/local/tomcat/native-jni-lib",
                "LD_LIBRARY_PATH=/usr/local/tomcat/native-jni-lib",
                "GPG_KEYS=48F8E69F6390C9F25CFEDCD268248959359E722B A9C5DF4D22E99998D9875A5110C01C5A2F6059E7",
                "TOMCAT_MAJOR=11",
                "TOMCAT_VERSION=11.0.1",
                "TOMCAT_SHA512=dce8800532c9dcb079d456e9ea561ac9b7c854a8c50dfcd78339d077f9db127d86dba339db3fcea16c75039c9201c3446ecd4807efe0d42fcf005d2061cbc090"
            ],
            "Cmd": [
                "catalina.sh",
                "run"
            ],
            "Image": "tomcat",
            "Volumes": null,
            "WorkingDir": "/usr/local/tomcat",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {
                "org.opencontainers.image.ref.name": "ubuntu",
                "org.opencontainers.image.version": "24.04"
            }
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "0165d2f0653c0007860103d17260eea569480b50e80e4c82e65d151a08223d07",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {
                "8080/tcp": [
                    {
                        "HostIp": "0.0.0.0",
                        "HostPort": "9090"
                    },
                    {
                        "HostIp": "::",
                        "HostPort": "9090"
                    }
                ]
            },
            "SandboxKey": "/var/run/docker/netns/0165d2f0653c",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "90879141fc32c7a0b75f38325398c70580db2113b626db20c48673d7cb09d10d",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "3e471403018bb920aacf144ae2d9e557259d5bdb827fbf6b47851c2eecf8fdf1",
                    "EndpointID": "90879141fc32c7a0b75f38325398c70580db2113b626db20c48673d7cb09d10d",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:02",
                    "DriverOpts": null
                }
            }
        }
    }
]
```
