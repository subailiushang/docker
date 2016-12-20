#### 1. Docker info
######查看docker的基本配置信息和功能
```
[root@docker ~]# docker info
Containers: 7
 Running: 0
 Paused: 0
 Stopped: 7
Images: 4
Server Version: 1.12.5
Storage Driver: devicemapper
 Pool Name: docker-253:0-440-pool
 Pool Blocksize: 65.54 kB
 Base Device Size: 10.74 GB
 Backing Filesystem: xfs
 Data file: /dev/loop0
 Metadata file: /dev/loop1
 Data Space Used: 2.059 GB
 Data Space Total: 107.4 GB
 Data Space Available: 14.81 GB
 Metadata Space Used: 4.018 MB
 Metadata Space Total: 2.147 GB
 Metadata Space Available: 2.143 GB
 Thin Pool Minimum Free Space: 10.74 GB
 Udev Sync Supported: true
 Deferred Removal Enabled: false
 Deferred Deletion Enabled: false
 Deferred Deleted Device Count: 0
 Data loop file: /var/lib/docker/devicemapper/devicemapper/data
 WARNING: Usage of loopback devices is strongly discouraged for production use. Use `--storage-opt dm.thinpooldev` to specify a custom block storage device.
 Metadata loop file: /var/lib/docker/devicemapper/devicemapper/metadata
 Library Version: 1.02.135-RHEL7 (2016-09-28)
Logging Driver: json-file
Cgroup Driver: cgroupfs
Plugins:
 Volume: local
 Network: overlay null host bridge
Swarm: inactive
Runtimes: runc
Default Runtime: runc
Security Options: seccomp
Kernel Version: 3.10.0-514.el7.x86_64
Operating System: CentOS Linux 7 (Core)
OSType: linux
Architecture: x86_64
CPUs: 2
Total Memory: 976.5 MiB
Name: docker
ID: 75FD:ZXWS:EON5:LRUX:6KHN:44S4:FU3Z:K2O3:E7UL:VQIN:4BYK:WO77
Docker Root Dir: /var/lib/docker
Debug Mode (client): false
Debug Mode (server): false
Registry: https://index.docker.io/v1/
WARNING: IPv4 forwarding is disabled
WARNING: bridge-nf-call-iptables is disabled
WARNING: bridge-nf-call-ip6tables is disabled
Insecure Registries:
 127.0.0.0/8
```

#### 2. docker pull 
###### 下载一个docker镜像文件（从指定的docker hub中下载，默认下载为最新版本）
```
[root@docker ~]# docker pull ubuntu
Using default tag: latest
latest: Pulling from library/ubuntu
b3e1c725a85f: Pull complete 
4daad8bdde31: Pull complete 
63fe8c0068a8: Pull complete 
4a70713c436f: Pull complete 
bd842a2105a8: Pull complete 
Digest: sha256:dbe36a89ad8daf8bbd2a68f14eab18b969d3f125104da51df6337bbf08d1c8ae
Status: Downloaded newer image for ubuntu:latest
```

#### 3. docker images
###### 查看下载完成的docker容器镜像文件
```
[root@docker ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              latest              104bec311bcd        4 days ago          128.9 MB
```

#### 4. docker run 
####### 运行第一个docker容器
-i ：开启标准输入stdin
-t ：开启tty，分配伪终端
```
[root@docker ~]# docker run -it ubuntu /bin/bash
root@64fb61c69b66:/# 
```

#### 5. docker ps -a
###### 查看容器列表
```
[root@docker ~]# docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                        PORTS               NAMES
d93f8ef79dc3        ubuntu              "/bin/bash"              3 minutes ago       Exited (0) 2 seconds ago                          pedantic_chandrasekhar
64fb61c69b66        ubuntu              "/bin/bash"              7 minutes ago       Exited (0) 7 minutes ago                          big_wing
e9547d50e6cc        ubuntu              "/bin/bash"              8 minutes ago       Exited (127) 7 minutes ago                        nostalgic_ramanujan
402f16d2f8d3        ubuntu              "/bin/bash"              8 minutes ago       Exited (0) 8 minutes ago                          elegant_lamarr
```

#### 6. docker run --name
--name ：给容器指定名称
```
[root@docker ~]# docker run --name ubuntu_test -it ubuntu /bin/bash
root@cada165ed6bf:/# exit
exit
[root@docker ~]# docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                          PORTS               NAMES
cada165ed6bf        ubuntu              "/bin/bash"              6 seconds ago       Exited (0) 3 seconds ago                            ubuntu_test
```

#### 7. docker start +[容器名称|容器ID]
###### 启动容器
```
[root@docker ~]# docker start ubuntu_test
ubuntu_test
[root@docker ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
cada165ed6bf        ubuntu              "/bin/bash"         2 minutes ago       Up 9 seconds                            ubuntu_test
```

#### 8. docker attach +[容器名称|容器ID]
###### 附着或者进入到容器中，沿用docker run时的/bin/bash交互模式
```
[root@docker ~]# docker attach ubuntu_test
^C
root@cada165ed6bf:/# 
```

#### 9. docker run -d
###### 创建守护式容器
一个长期运行的容器，大多数时候我们需要一个在后台长期运行的容器，而不是使用exit后就自动停止的容器
```
[root@docker ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
[root@docker ~]# docker run -itd ubuntu /bin/bash
ecc5f40d8f02021cf01dd15bc5c443392667ef96fd86a93f0659d76e771d7464
[root@docker ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
ecc5f40d8f02        ubuntu              "/bin/bash"         4 seconds ago       Up 3 seconds                            jolly_goldwasser
```

#### 10. docker logs
###### 查看容器内部的日志
```
[root@docker ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
ecc5f40d8f02        ubuntu              "/bin/bash"         2 minutes ago       Up 2 minutes                            jolly_goldwasser
[root@docker ~]# docker logs ecc
```

#### 11. docker top
###### 查看容器内部的进程
```
[root@docker ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
ecc5f40d8f02        ubuntu              "/bin/bash"         3 minutes ago       Up 3 minutes                            jolly_goldwasser
[root@docker ~]# docker top ecc
UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
root                15927               15913               0                   20:56               pts/1               00:00:00            /bin/bash
```

#### 12. docker exec 
###### 在容器内部运行进程
* 后台任务
* 交互式任务
```
[root@docker ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
ecc5f40d8f02        ubuntu              "/bin/bash"         6 minutes ago       Up 6 minutes                            jolly_goldwasser
[root@docker ~]# docker exec -d ecc touch /etc/a.txt
[root@docker ~]# docker exec -it ecc /bin/bash
root@ecc5f40d8f02:/# ls /etc/a
a.txt         adduser.conf  alternatives/ apt/          
root@ecc5f40d8f02:/# ls /etc/a.txt 
/etc/a.txt
```

#### 13. docker stop
###### 停止容器
```
[root@docker ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
ecc5f40d8f02        ubuntu              "/bin/bash"         8 minutes ago       Up 8 minutes                            jolly_goldwasser
[root@docker ~]# docker stop ecc
ecc
[root@docker ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

#### 14. docker inspect
###### 对容器进行详细的检查，返回众多的配置信息
```
[root@docker ~]# docker inspect ecc
[
    {
        "Id": "ecc5f40d8f02021cf01dd15bc5c443392667ef96fd86a93f0659d76e771d7464",
        "Created": "2016-12-20T12:56:09.163454397Z",
        "Path": "/bin/bash",
        "Args": [],
        "State": {
            "Status": "exited",
            "Running": false,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 0,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2016-12-20T12:56:10.275497292Z",
            "FinishedAt": "2016-12-20T13:04:33.326874088Z"
        },
......
```

#### 15. docker rm + 容器
###### 删除一个容器
```
[root@docker ~]# docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                        PORTS               NAMES
ecc5f40d8f02        ubuntu              "/bin/bash"              15 minutes ago      Exited (0) 6 minutes ago                          jolly_goldwasser
cada165ed6bf        ubuntu              "/bin/bash"              23 minutes ago      Exited (130) 15 minutes ago                       ubuntu_test
[root@docker ~]# docker rm ecc
ecc
[root@docker ~]# docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                        PORTS               NAMES
cada165ed6bf        ubuntu              "/bin/bash"              23 minutes ago      Exited (130) 15 minutes ago                       ubuntu_test
```

#### 16. docker rmi + 镜像
###### 删除一个镜像
在删除镜像之前必须删除基于该镜像的容器
也可以加入参数 -f 强制删除该镜像文件
```
[root@docker ~]# docker rmi ubuntu
Error response from daemon: conflict: unable to remove repository reference "ubuntu" (must force) - container 402f16d2f8d3 is using its referenced image 104bec311bcd
[root@docker ~]# docker rm 402
402
[root@docker ~]# docker rmi ubuntu
Error response from daemon: conflict: unable to remove repository reference "ubuntu" (must force) - container e9547d50e6cc is using its referenced image 104bec311bcd
[root@docker ~]# docker rmi -f ubuntu
Untagged: ubuntu:latest
Untagged: ubuntu@sha256:dbe36a89ad8daf8bbd2a68f14eab18b969d3f125104da51df6337bbf08d1c8ae
Deleted: sha256:104bec311bcdfc882ea08fdd4f5417ecfb1976adea5a0c237e129c728cb7eada
[root@docker ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
```

