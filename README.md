Trojan Install Introduction
----------------------------

**!!!Don't Fork and Don't Star!!!**

**!!!请不上Fork！也请不要Star!!!**


## 安装方法

### 1. 准备服务器

准备号一台公网可以访问的，可以科学上网的服务器，推荐使用Google Cloud的虚拟机实例，没有带宽限制，而且还便宜

### 2. 准备一个域名

在外网购买一个无需备案的域名，推荐： https://www.namesilo.com/ ,域名购买以后将域名解析到Step1准备的服务器，最后是解析一个二级域名指向服务器。

### 3. trojan安装

使用SSH登录服务器，接下来的所有操作都是在服务器终端完成的

### 4. 切换到root账户

Trojan的安装都是在root账户下完成的，需要首先切换到root账户下

```
sudo -i
```

如果忘记了root账户的密码，可以使用下面的命令重置root账户的密码:

```
sudo passwd
```

### 5. 安装Trojan

这里推荐使用centos7进行Trojan部署，如果使用的是centos7的话，直接root账户下在终端中输出下面的命令:

```
curl -O https://raw.githubusercontent.com/ShawnZhang31/troooojan-install/main/trojan_centos7.sh && chmod +x trojan_centos7.sh && ./trojan_centos7.sh
```

如果是其他的系统如：Ubuntu、Debian可以使用如下命令:

```
curl -O https://raw.githubusercontent.com/ShawnZhang31/troooojan-install/main/trojan_mult.sh && chmod +x trojan_mult.sh && ./trojan_mult.sh
```

回车之后，会出现选择菜单，选择第1项，安装trojan.

在Trojan的安装过程中需要输入解析到此VPS的域名，所以一定要保证Step2中的域名正确解析到服务器。

安装完成之后，会给出trojan-cli.zip的下载地址，记得需要把这个文件夹下载下来,解压之后里面有一个config.json文件夹，这是访问trojan服务器的配置，非常重要！！！

可以通过 https://github.com/trojan-gfw/trojan/releases 更新trojan-cli客户端，但是config.json只能从服务器上下载。

如果忘记下载地址，可以通过在服务器上的`/usr/src`目录下下载`trojan-cli.zip`

### 6. 安装BBRplus加速

使用BBRplus可以提高Trojan的代理的速度，方位YouTube的8K视频毫无压力。

依然是在root账户下在终端中输入:

```
wget -N --no-check-certificate "https://raw.githubusercontent.com/ShawnZhang31/Linux-NetSpeed/main/tcp.sh"
chmod +x tcp.sh
./tcp.sh
```

命令执行后，出现选项，输入2选择安装BBRPlus加速器，安装完成之后输出y重启服务器。

待服务器重启之后，重新ssh登录服务器，进入root账户下，重新输入:

```
wget -N --no-check-certificate "https://raw.githubusercontent.com/ShawnZhang31/Linux-NetSpeed/main/tcp.sh"
chmod +x tcp.sh
./tcp.sh
```

出现选择界面后，输入7，启用BBRPlus加速器，自此Trojan部署完毕。

### 7. Trojan的使用

使用trojan-cli在本地连接Trojan服务器，设置本地网络的socks5全局代理，或者使用Chromium浏览器可以使用SwithyOmega_Chromium.crx扩展只进行浏览器代理。

更多使用说明可以观看[视频](./tutorials/trojan_win_android_ios.mp4)

<div style="text-align:center;">
    <h6>Trojan客户端全平台使用教程</h6>
    <video width="80%" controls>
        <source src="./tutorials/trojan_win_android_ios.mp4" type="video/mp4"/>
        当前浏览器不支持视频播放，可以通过以下链接查看:
        <p><a href="https://www.youtube.com/watch?v=shnA4Tdsnbw&t=919s">Youtube</a></p>
        <p><a href="./tutorials/trojan_win_android_ios.mp4">视频地址</a></p>
    </video>
</div>

## 注意

### 1. trojan-cli提示SSL连接问题

由于当前的脚本在安装Trojan的时候，自动生成了ssl证书并进行部署，但是这个证书只有3个月的有效期，3个月之后，可能trojan-cli就提示因为无法验证证书而不能连接服务器。此时登录服务器重新安装一下Trojan即可。
