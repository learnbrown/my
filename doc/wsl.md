# Windows Subsystem for Linux(WSL) 的安装及配置教程

## 使用wsl指令安装linux
使用cmd或powershell输入以下指令后，windows系统将自动开始下载ubuntu并开始安装 <br />
在指令后添加 --web-download 可以加速国内网络下的下载速度 <br />
```shell
wsl --install --web-download
```
默认安装为ubuntu系统，也可自己选择其他版本进行安装<br />
这里我已经安装过ubuntu，所以选择安装ubuntu24.04版本进行演示<br /> 
```shell
wsl --list --online #查询可以安装的系统版本
wsl --install <系统名（省略则默认安装ubuntu）> --web-download
```
![img1.png](/doc/img/241029/img1.png)
下载安装完成后，将自动在终端中打开ubuntu子系统并开始初始化 <br />
输入用户名及密码来设置账户，在linux中输入密码时看上去不会有任何显示，但实际上是有在正常地输入<br />
创建完成账户后子系统的安装便结束了，可以直接在windows中便捷地使用linux操作系统<br />

## 为apt换源为国内镜像站
apt是用于管理Ubuntu中软件包的命令行工具，ubuntu中应用的安装都需要使用到他，不过apt的默认源为国外的网站，将其更换为国内镜像源使用起来会更为便利<br />
```bash
cd /etc/apt/sources.list                //打开apt配置文件所在目录
sudo chmod 777 sources.list             //由于配置文件为只读权限，需先修改访问权限
sudo cp sources.list sources.list.copy  //备份原配置文件
vim sources.list                        //使用vim编辑
```
进入vim后，初始为命令模式，可以使用指令```dd```对一整行进行剪切操作，这里我们使用该命令快速地将原来的内容清除，之后按下```i```键进入插入模式，此时就能像使用记事本一样在文件中输入字符，我们复制以下内容后按下右键即可复制到文件中<br />
```
deb https://mirrors.aliyun.com/ubuntu/ jammy main restricted universe multiverse
deb-src https://mirrors.aliyun.com/ubuntu/ jammy main restricted universe multiverse

deb https://mirrors.aliyun.com/ubuntu/ jammy-security main restricted universe multiverse
deb-src https://mirrors.aliyun.com/ubuntu/ jammy-security main restricted universe multiverse

deb https://mirrors.aliyun.com/ubuntu/ jammy-updates main restricted universe multiverse
deb-src https://mirrors.aliyun.com/ubuntu/ jammy-updates main restricted universe multiverse

# deb https://mirrors.aliyun.com/ubuntu/ jammy-proposed main restricted universe multiverse
# deb-src https://mirrors.aliyun.com/ubuntu/ jammy-proposed main restricted universe multiverse

deb https://mirrors.aliyun.com/ubuntu/ jammy-backports main restricted universe multiverse
deb-src https://mirrors.aliyun.com/ubuntu/ jammy-backports main restricted universe multiverse

```
这里其实是将原来apt的源更换为国内的阿里云镜像源<br /><br />

换源后还需更新apt的列表
```bash
sudo apt --update
```
更新apt列表后才能正常的开始使用apt下载应用<br /><br />
以下是apt中常用的指令
```bash
更新系统中的应用
sudo apt --upgrade
```
```bash
下载应用（例如下载net-tools）
sudo apt --install net-tools
```