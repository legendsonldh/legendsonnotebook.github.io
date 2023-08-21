# Structurizr可视化安装指南

本篇文章将总结Structurizr这一工具可视化安装指南。

## C4 Model

structurizr工具是用于画架构的，这种架构不同于一般的软件架构，而是针对于复杂系统，层层递进的C4 Model架构，关于C4 Model 可以参考以下资料：

1. [C4 Model Homepage](https://c4model.com/)
2. [Document architectures by using the C4 model](https://www.ibm.com/garage/method/practices/code/c4-model-for-software-architecture/)

下面简要介绍一下C4 Model的分层，引用官网的一张图，我们可以发现，C4 Model有着层层递进的架构，非常适合用于开发系统架构：

![C4Model](https://c4model.com/img/c4-overview.png)

这里再给出一个链接，是我认为C4 Model最好的一个范例：

[Big Bank plc - Internet Banking System](https://structurizr.com/share/36141/)

但是 C4 Model是理论上对相关的架构进行了定义，我们还需要能够实现的工具，经过比较，我选择了Structurizr工具，该工具的理念为All in Code，即使用代码生成图片。

## Structurizr

[Structurizr](https://structurizr.com)工具最好的实践方式如下： 

> Structurizr CLI(命令行转换工具) + Structurizr On-premises（Web Server）

我们使用Structurizr CLI将dsl文件上传到Structurizr On-premises中解析，然后在Web端对架构图进行浏览。

### Structurizr On-premises安装

参考[官方文档](https://structurizr.com/share/18571/documentation)，步骤如下：

```bash
docker pull structurizr/onpremises
docker --restart always --detach --rm -p 8080:8080 -v PATH:/usr/local/structurizr structurizr/onpremises
```

Docker部署后访问对应端口即可，初始账户和密码如下：

>Username: structurizr
> 
>Password: password

### Structurizr CLI安装

其中Structurizr CLI是一个命令行转换工具，用于将你编写的dsl文件转换成C4Model的图，安装方式如下：

1. 从[Structurizr CLI的GitHub仓库](https://github.com/structurizr/cli)中下载最新的release压缩包
2. 解压到你常用的地方
3. 使用如下命令将dsl文件上传,PS 该命令可以在Structurizr On-premises的Workspace中的Settting界面找到

```bash
structurizr -url http://localhost:6060/api -id 2 -key <KeyId> -secret <SecretId> -workspace <Your Dsl File Path>

```


