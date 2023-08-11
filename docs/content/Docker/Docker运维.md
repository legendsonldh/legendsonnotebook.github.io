# Docker运维

这里记录在运维Docker的过程中遇到的一些问题

> 问题一：Error response from Daemon:devmapper:Error mounting:invalid argument

今天对GitLab服务器进行了扩容，扩容需要重启服务器，起来以后发现docker起不来，然后发现gitlab服务也起不来，出现如下链接报错：

[Error response from Daemon:devmapper:Error mounting:invalid argument](https://topic.alibabacloud.com/a/error-response-from-daemondevmappererror-mountinginvalid-argument-when-starting-docker-container-error-resolution_1_12_30732732.html)

上面这个问题，发现解决方案确实如下所说，不过值得注意的一点：两个操作都需要执行：

```text
a. You can reset the SELinux to enable and then restart the physical machine to fix it.
b. Modifies the configuration of the container. For example, the configuration of my container is a 
/var.lib/docker/containers/e7ef71494940ba293be4b3f74198bf34835c35537810053b051d9a6c33adbd32/config.v2.json file. 
"MountLabel": "system_u:object_r:svirt_sandbox_file_t:s0:c12,c257", 
"ProcessLabel": "system_u:system_r:svirt_lxc_net_t:s0:c12,c257"Modify the rebuild to, and "MountLabel": "", 
"ProcessLabel": "" then restart the Docker daemon, the container can be repaired.
```

参考链接：
1. https://blog.csdn.net/gpdsjqws/article/details/123656697

> 问题2： exec  user process caused  "permission  denied"

又遇到了个重启的问题

1. 关闭selinux

```bash
setenforce 0
```

2. 修改`/etc/selinux/config/`文件，将`SELINUX=enforcing`改为`SELINUX=disabled`


参考链接：
1. https://blog.csdn.net/shenhonglei1234/article/details/86305802

2. https://blog.csdn.net/kai172142xiang/article/details/81436485


> 问题3： Error response from daemon: failed to listen to abstract unix socket

解决方案，我们找到docker容器的PID，把它删除

1. 查找PID
```bash
netstat -lnp | grep <containerid>
```

我们会看到如下：
```bash
unix ..  [ACC] STREAM  LISTENING 12222  231/containerd
```
其中231就是PID


2. 杀掉重启

```bash
kil 231
docker start
```


