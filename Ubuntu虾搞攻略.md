# Ubuntu虾搞攻略
## 1. 备份
一定要备份,不然搞坏就凉凉.当然你要是有钱搞个测试机，当然再好不过，在虚拟机里面搞，也是可以的。
在搞机之前一定要认识到搞机的风险,部分机型是不支持你安装的,目前是带有x86架构的电脑,才支持安装Ubuntu系统,请谨记
备份建议备份在"非系统盘"、"加密存储介质"、"个人云盘的隐藏文件夹"。

![](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1572439499599&di=05adeed63ffdac3e370ebbc750d6d730&imgtype=0&src=http%3A%2F%2Fp.ssl.qhimg.com%2Ft0183821e65cd66384d.png)

## 2.安装
系统镜像下载（非Ubuntu系统）
 	官方镜像地址http://mirrors.melbourne.co.uk/ubuntu-releases/
系统建议	
    Ubuntu18.04以前的系统已经过去不适合开发
    Ubuntu18.10 已关闭服务
    当前Ubuntu19.04已经可以投入正常使用
    19.10尚在个人测试中，已知的是启动速度相较于以前的版本更快。

![Ubuntu1904](https://www.linuxidc.com/upload/2019_04/19041906287715.png)

Ubuntu系统的准备

- 把Python的软连接指向修改为原来自带的Python的版本即Python2.7

```
python2 -V  # 查看当前系统自带Python2的版本
sudo ln -s /usr/bin/python2.7 /usr/bin/python  # 修改当前的Python指向
# 如果出错，已经存在
sudo rm /usr/bin/python  #再进行如上步骤
# 如果已经丢失Python
sudo apt-get install --reinstall python-minimal
sudo apt-get install --reinstall python2.7
```

- 修改设置

  > software&Updates -> Updtaes -> Notify me of a new Ubuntuversion:For  any new  version

- 打开软件更新

  ###### 按更新指示更新、给权限即可

- 制作启动盘（非Ubuntu）
  1. 需要一个制作启动盘的软件，如rufus，一个8G大小的U盘
  2. 使用软件把下载的镜像刻录在U盘里

- 重启

  1. U盘插入最快速的一个USB接口，重启电脑，修改BIOS

     关闭security boot、关闭PTT(Dell的机型有此设置)、设置U盘启动，保存并退出

  2. 进入安装界面，按指示或者如下教程安装即可（单系统安装直接格式系统盘安装，双系统要提前分区好并格式化）

  ​       [安装教程](https://www.jianshu.com/p/54d9a3a695cc)

## 3. 换源

*众所周知，国外的软件源，多数是卡得不行或者连不上的，为了能够正常使用这个系统，我们需要更快更好的软件源，阿里云就是个更好的选择*

> 第一步肯定是备份

```
sudo -s
cd /etc/apt/
cp sources.list sources.list.bak
```

> 第二部就直接上手改源了

```
vim sources.list
把源修改为如下内容：
deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe
multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe
multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
保存修改后
apt update       更新源
apt upgrade      更新软件
```

## 4. 输入法

没得输入法，怎么能在linux的环境里口吐芬芳呢？

```
apt install f citx -y
```

装完之后，在设置的Region & Language选项中把Keyboard input method system改为fcitx

下载一波搜狗linux输入法

   [搜狗输入法](https://pinyin.sogou.com/linux/)

安装成功后重启，如果出错，运行sudo apt --fix-broken install

重启完后，系统的右上角菜单里会出现一个小键盘，点击Configure Current Input Method,添加搜狗输入法。

再尝试打字，如果失败，重启电脑，多试几次。

## 5. 桌面图标

刚用Ubuntu的时候，有些软件是没有图标的，启动要去找到对应的文件夹，对此表示同情。

![](http://5b0988e595225.cdn.sohucs.com/images/20190207/18b23b33dece4e699bbe8fa5a6f46f60.jpeg)

但是，这个是能解决的！

以idea为例，我们进行一波操作

首先，在官网下载它的安装包[idea](https://www.jetbrains.com/)

然后

```
cd /home/dev/Downloads
tar -zxvf idea20198.tar.gz
sudo mv /idea /usr/loacal
到这里基本上是安装成功了，但是还没有桌面图标
cd /usr/share/applications
这里面有好几个桌面图标，我们可以复制一个来作为自己的桌面图标
cp fcitx.desktop idea.desktop
接下来就是编辑我们自己的图标了（没有vim的sudo apt-get install vim一下）
sudo vim idea.desktop
这个时候复制的桌面图标是很多杂乱行的
Name=Fcitx
    Name[ca]=Fcitx
    Name[da]=Fcitx
    Name[de]=Fcitx
    Name[es]=Fcitx
    Name[ja]=Fcitx
    Name[ko]=Fcitx
    Name[ru]=Fcitx
    Name[zh_CN]=Fcitx
    Name[zh_TW]=Fcitx
    GenericName=Input Method
    GenericName[ca]=Mètode d'entrada
    GenericName[da]=Inputmetode
    GenericName[de]=Eingabemethode
    GenericName[es]=Método de entrada
    GenericName[ja]=入力メソッド
    GenericName[ko]=입력기
    GenericName[ru]=Метод ввода
    GenericName[zh_CN]=输入法
    GenericName[zh_TW]=輸入法
    GenericName[zh_TW]=輸入法
    Comment=Start Input Method
    Comment[ca]=Inicia el mètode d'entrada
    Comment[da]=Start inputmetode
    Comment[de]=Eingabemethode starten
    Comment[ja]=入力メソッドを開始
    Comment[ko]=입력기 시작
    Comment[ru]=Запустить метод ввода
    Comment[zh_CN]=启动输入法
    Comment[zh_TW]=啓動輸入法
Exec=fcitx
Icon=fcitx
Terminal=false
Type=Application
    Categories=System;Utility;
    StartupNotify=false
    X-GNOME-AutoRestart=false
    X-GNOME-Autostart-Notify=false
    X-KDE-autostart-after=panel
    X-KDE-StartupNotify=false
去掉那些被缩进的地方
Name=Fcitx    这里是app的名称
Exec=fcitx    这个是app里面bin文件夹下叫xx.shh或者xx的启动程序
Icon=fcitx    这个是你自己选择的app展示的图标，暂时只支持png格式（idea有自带图标）
Terminal=false  为true的时候每次打开app会弹一个终端窗，建议false
Type=Application   类型，app，默认即可
修改之后
Name=idea
Exec=/usr/local/idea2019/bin/idea.sh
Icon=/usr/local/idea2019/bin/idea.png    
Terminal=false  
Type=Application
```

这个时候保存了，这就算创建成功了
但是我们还需要有一步操作，找到文件管理器的图标，进入刚刚的/usr/share/applications，找到我们刚刚创建的桌面图标

把它拖到桌面上，是的，你没有听错，把它拖到桌面上，双击，这个时候会出现一个弹窗，点击trust and luanch，成功进入程序后，大功告成

![](http://pic4.zhimg.com/v2-8d2c1b292bb8a2ad6cf3544fa0e31327_b.png)

什么，你还想把它放在任务栏？没问题啊，找到任务栏上面app的图标，右键菜单里，点击add to favorite ，这就ok了！

## 6. 美化

到这里你也发现了，Ubuntu这个基佬紫的魔幻配色，实在是辣眼睛，所以国内大佬们各显神通，推荐了以下几种美化方式

- Gnome Twaek

  ​	这是个神奇的软件，在软件中心就能搜到，也可以

  ```
      sudo apt-get update
      sudo apt-get install gnome-tweak-tool
  ```

  参考[教程](https://blog.csdn.net/lishanleilixin/article/details/80453565)

  分享一个[主题下载网站](https://www.pling.com/s/Linux/browse/cat/366/order/latest/)，有logo的，界面的。

  此外，有一点警告，登录界面和开机界面，不要轻易改，改主题就行了，千万别作死，一作就死。

- budgie桌面

  ​	Linux 中有许多桌面环境。从易于使用并有令人惊叹图形界面的 [GNOME 桌面](https://www.gnome.org/)（在大多数主要 Linux 发行版上是默认桌面）和 [KDE](https://www.kde.org/)，到极简主义的 [Openbox](http://openbox.org/wiki/Main_Page)，再到高度可配置的平铺化的 [i3](https://i3wm.org/)，有很多选择。我要寻找的桌面环境需要速度、不引人注目和干净的用户体验。当桌面不适合你时，很难会有高效率。

  ​	Budgie桌面环境是Evolve OS发行版的默认桌面环境，而且是Evolve OS的一个项目。Budgie桌面环境的设计，专注于潮流人士，设计更为小巧、优美而简约。Budgie最难能可贵的一点，是他不亦步亦趋的精神，从设计之初，便从头开始，集思广益，使用了包GTK和其他比如Vala和C语言，设计出了独一无二的优秀桌面环境！

  ​	Budgie 与GNOME stack进行了紧密的集成，通过底层技术的改进，从而开发出了优秀的可替代的桌面环境。它同样是为开源而生，所以一样可以在其他发行版上完美使用。有一点也很有爱，Budgie如今也可以通过设置面板选项，使得看起来很像大家最爱的GNOME 2样式。现在的Budgie正在紧锣密鼓的保持开发，代码已经托管在了[GitHub](https://github.com/evolve-os/budgie-desktop)，大家也可以通过编写代码，报告BUG，一起为Budgie的发展做出贡献。

  所以这里给大家准备了两种安装方式：

   - 命令行安装

     ```
     sudo apt update && sudo apt upgrade apt update && sudo apt upgrade
     sudo apt install ubuntu-budgie-desktop apt install ubuntu-budgie-desktop
     ```

     下载完成后，你将看到选择显示管理器的提示。选择 “lightdm” 以获得完整的 Budgie 体验。

     ![](https://ss.csdn.net/p?https://mmbiz.qpic.cn/mmbiz_png/W9DqKgFsc68rLbNzWWYaGhoiab0ZpOgbV91ytmewXDalmmtUFWBPicJ7v5KtleXNpOZ8DvOl5QE83icDTlDTdy3cg/640?wx_fmt=png)

     完成重启后，开机就会看到budgie的登录界面啦

   - iso安装，目前已有最新的[Ubuntu Budgie 19.04](http://cdimage.ubuntu.com/ubuntu-budgie/releases/19.04/release/ubuntu-budgie-19.04-desktop-amd64.iso)可用,按刷机的方式操作，一样可以有此种体验

     ![](http://b-ssl.duitang.com/uploads/item/201707/13/20170713104223_dYXR3.jpeg)

- 其他的桌面还没体验过，后续会陆续添加。

## 7.虚拟机

Ubuntu是没有专门的微信可以用的，即使是electric-wechat，也不过是个网页版的本地端，造成了很多不变，这就需要我们搞一个Windows虚拟机了。

​		Ubuntu 18.04这类长期使用的系统，安装到使用是没有什么问题的，但是从18.10开始，渐渐会出现一些问题，这次我们就来想办法搞他一波：

​		18.10：一般在18.10系统中[VMware](https://www.vmware.com/cn/products/workstation-pro/workstation-pro-evaluation.html)安装完打开后,会出现要你安装什么什么包的提示，而且几乎不会成功，经过多次在虚拟机测试，发现是缺少gcc的包。

​		gcc这个沙雕东西，一般是系统自带的，但是总是会有报错的机会，GCC(GNU编译器集合）许多 C,C++,GNU工具和大多数的开源项目，包括linux内核都是由GCC编译而来，所以不修复它是完全不行的。

教程如下或参阅[csdn教程](https://blog.csdn.net/qq_43504064/article/details/101010507)	

```
sudo apt update
sudo apt install build-essential
验证一波
gcc --version
结果是
gcc (Ubuntu 8.3.0-6ubuntu1) 8.3.0
Copyright (C) 2018 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

```

​		19.04: 1904的系统中，内核也做了升级，已经是5.0的内核了，相较于以前的系统有所不同，所以也会有内核导致的安装异常，但是不用慌，[mkubecek](https://github.com/mkubecek/vmware-host-modules)大佬有办法。

​		代码如下：

```
git clone -b workstation-15.0.2 https://github.com/mkubecek/vmware-host-modules.git
cd vmware-host-modules
tar -cf vmmon.tar vmmon-only
tar -cf vmnet.tar vmnet-only
sudo cp -v vmmon.tar vmnet.tar /usr/lib/vmware/modules/source/
sudo vmware-modconfig --console --install-all
```

另外，如果觉得搞虚拟机太麻烦，想把它卸载掉，参照下方代码：

```
sudo vmware-installer -u vmware-workstation
```

转载于：https://blog.csdn.net/weixin_30678821/article/details/98999968

![](http://i0.hdslb.com/bfs/article/9a8c23c5c1c16d15544670c87020d96d745b4738.jpg)

## 8. 死亡操作

此处记载本人多次导致系统爆炸的操作

- 安装显卡驱动

  在18.04这样的系统里，NVIDIA的驱动，千万别碰，再三警告，别虾搞，搞的下场就是：

  ![](http://i0.hdslb.com/bfs/article/fb83cf1cddfe33479e1705c4909fdf091daaefa0.jpg)

  玩一波梗

- 修改开机界面图和登录界面图

  ​	美化的操作是个风险极大的操作,再次建议，美化主题得了，别搞事，风险很大，说不定哪一次重启的时候，你会发现图形界面没了

  ​		传统操作是这样

  ```
  按 ctrl+alt+F1（进入命令行界面）
  登录
  sudo apt-get update
  sudo apt-get install --reinstall ubuntu-desktop
  sudo apt-get install unity
  sudo service lightdm resta
  ```

  如果不行，我能力有限，建议重装吧。

- rm -rf /*

   大佬们是懂的，小白听说了应该也要引起重视。详情见[linux执行rm -rf /*命令后的效果原来是这样](https://www.daixiaorui.com/read/265.html)

   警告：不要在生产设备上试，到时候你删库了，是来不及跑路的！

   别从面向对象编程变成面向监狱编程。

  ​	破坏有多大，大概是下图这么大：

  ![](https://pics5.baidu.com/feed/80cb39dbb6fd52669d3920c95071fc2fd507364e.jpeg?token=67050943f99f3cbce3862d3a2d349515&s=08B2379A48BE768C5EF19CD8030040B1)

  ![](https://pics0.baidu.com/feed/a8773912b31bb051a7e5c084cc13b1b048ede0c3.jpeg?token=2c38e485295273039e6cefe3e536b396&s=2B008B4FCC3427860338D4A80300E093)

  ​			![](https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=2078211895,2757343463&fm=26&gp=0.jpg)

## 最后



![](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1572514342849&di=baf7e87d48ef0be7dffa1d62386ef6f8&imgtype=0&src=http%3A%2F%2Fb-ssl.duitang.com%2Fuploads%2Fitem%2F201812%2F10%2F20181210095624_ndyab.png)

 

