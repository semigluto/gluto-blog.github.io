# Docker使用笔记
## [2/27]
**安装Docker:**  
执行命令```sudo apt-get -y install docker.io```
结果报错了：  
*The following packages have unmet dependencies:  
docker.io : Depends: containerd (>= 1.2.6-0ubuntu1~)  
E: Unable to correct problems, you have held broken packages.*  
网站https://blog.csdn.net/u012921921/article/details/116259208 未成功，但是教程很好  
**于是找了另外一个教程，执行以下命令安装docker的依赖项：**  
```apt-get install ca-certificates curl gnupg lsb-release```  
然后添加docker GPG密钥：  
```curl -fsSL http://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -```
安装docker软件源：  
```sudo add-apt-repository "deb [arch=amd64] http://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"```  
安装docker:  
```apt-get install docker-ce docker-ce-cli containerd.io```  
将用户添加到docker用户组（注意要重新登陆）：  
```sudo usermod -aG docker $USER```  
重启docker：  
```service docker restart```  
检验是否成功：  
```sudo docker run hello-world```  
最后成功了，然后再查看以下docker版本：  
```sudo docker version```
输出如下，正常：  
*Version:           25.0.3  
 API version:       1.44  
 Go version:        go1.21.6  
 Git commit:        4debf41  
 Built:             Tue Feb  6 21:14:17 2024  
 OS/Arch:           linux/amd64  
 Context:           default*  
成功的网站：https://zhuanlan.zhihu.com/p/651148141
## [2/28]
**Docker生成一个虚拟化的空间（容器）**，提供给你一个运行程序的的地方
Docker十分方便，比传统的虚拟机要好很多。 
Docker优点：  
执行速度快  
占用内存少  
更容易迁移和维护  
理解Docker需要理解容器，镜像，和仓库这三个概念  
**Docker镜像(Image)**是一个特殊的文件系统，提供了容器需要运行的各种程序，库，资源，或配置等文件和其参数  
**Docker容器(Container)**和镜像的关系，就像c++面向对象里的类和实例一样（很好的例子）。
容器是镜像运行的实体，容器可以被创建、启动、停止等。  
**Docker仓库(Repository)**是一个存储镜像的地方，仓库中包含对应着镜像的标签。  

运行容器需要在本地存在对应的镜像，如果不存在镜像，docker将从镜像仓库下载。 
从docker仓库获取镜像并下载到本地：
```docker pull [选项] [Docker Registry 地址[:端口号]/]仓库名[:标签]```
比如：
```docker pull ubuntu:20.04```  
我这边成功了，压缩的镜像只有27MB，然后运行镜像：  
```docker run -it --rm ubuntu:20.04 bash```  
然后在运行程序里输入：
```cat /etc/os-release```  
这将会输出镜像的相关信息  
最后输入```exit```就能退出程序了  
上述教程记笔记的网址：https://docker-practice.github.io/zh-cn/
