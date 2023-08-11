# Centos下Docker安装

本篇将总结Centos或一些Linux系统下安装Docker的方式

## 在线

如果是在线情况下，使用apt rpm等包管理器安装即可。

## 离线

离线安装和在线安装最大的不同在于包的依赖，离线需要把所有的依赖都安装一遍，较为繁琐。

**Step1**: 我们得找到docker的库去下每个依赖包：

> https://download.docker.com/linux/centos/7/x86_64/stable/Packages/

Note: 注意，如果是Windows系统的话，可以用WSL子系统运行以下命令下载rpm包。

```bash
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
yumdownloader --resolve docker-ce docker-ce-cli containerd.io
```

**Step2**: 把这些依赖包传到内网电脑中,使用rpm安装

1. 打包下载的包

```bash
tar cf docker-ce.offline.tar *.rpm
```
2. 在内网电脑中解压

```bash
tar xf docker-ce.offline.tar
```
3. 安装Docker

```bash
sudo rpm -ivh --replacefiles --replacepkgs *.rpm
```

4. 启动dockerv
```bash
sudo systemctl start docker
```

### 可能的问题
> 问题1：安装rpm包时提示错误：依赖检测失败

这种时候我们使用强制安装命令，如下：

```bash
sudo rpm -ivh --replacefiles --replacepkgs *.rpm --nodeps --force
```

> 问题2：没有centos系统怎么办？

使用Docker在外网机上新拉个centos镜像即可

参考链接：
1. https://zhuanlan.zhihu.com/p/109480358
2. https://blog.csdn.net/GentleLin/article/details/90294324
3. https://cloud.tencent.com/developer/article/1701451