# Ubuntu Guide
	基于当前ubuntu系统旧文档的难度,对其进行补充和详细解释,另外在使用过程中遇到的各种报错排查,后期会陆续补全,也欢迎补充.
	遇到困难怎么办:https://stackoverflow.com/   搜一下
## 1. 环境配置
#### Java(JDK)
 - 下载,地址:http://jdk.java.net/archive/
 
 		目前由于oracle公司对jdk不再免费,所以我们使用openjdk来下载,版本为11.0.2
    
 -	解压(非root权限)
 	
    		为避免jdk解压复制后,idea读取jdk不能正常加入包或者拉取远程包,需要在非root权限下进行解压
    
    		解压命令为:   


          		tar -zxvf jdk的tar.gz文件
          
		或者使用右键点击压缩,选中"Extract Here",同样将文件解压到当前文件夹.
    
 - 复制(root权限)
 	
    	由于没有root权限无法复制文件到/usr这类文件夹下,此处使用root权限进行复制
    
    复制命令:   
    
        sudo cp 解压出的文件夹 /usr/local
     

 - 环境变量配置
   
	编辑profile文件:
    	 sudo cp /etc/profile  /etc/profile.bak 备份一波
    
         sudo vim /etc/profile
         
         
         报错没有vim时:    
	        sudo apt-get install vim    　
         按键盘上的insert或者Ins键开启插入模式
         往文件后方填入如下内容:
            export JAVA_HOME=/media/ljc/dev/backup/openjdk-11.0.2_linux-x64_bin/jdk-11.0.2
            export JRE_HOME=${JAVA_HOME}/jre  
            export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib  
            export PATH=${JAVA_HOME}/bin:$PATH
         此处"JAVA_HOME="后方路径为个人复制的jdk文件夹地址,仅供参考
         检查无误后,按Esc键,进入退出模式
         Shift+: 键,调出":"光标
         在":"后输入"wq"后回车(不想保存或重新编辑则输入"q!"之后回车)
         
            source /etc/profile (报错没有权限时前方加sudo)
 - 检查
  
 	输入:
 
  
      java -version
      
      
      显示内容如下示例所示,表明安装成功:
      penjdk version "11.0.2" 2019-01-15
	  OpenJDK Runtime Environment 18.9 (build 11.0.2+9)
	  OpenJDK 64-Bit Server VM 18.9 (build 11.0.2+9, mixed mode)
      
      
      PS:'多jdk需要切换的情况下,无需配置/etc/profile,将解压的jdk文件夹复制到/usr/loacal下即可,使用时用idea加载选中对应jdk的文件夹就行'
      
      
#### gardle(依赖管理)
 - 下载,地址:https://gradle.org/releases/
 
	目前对版本不做过多要求,更新后为5.3以上即可,也不用必须是最新的,在"Download: binary-only or complete"中
    选complete下载完整包
 
 - 解压
 
	同java,需要在非root状态下解压,命令相同
    
 - 复制
    
    同java,root权限复制.
    
 - 环境变量配置
 
	编辑profile文件:    
         sudo vim /etc/profile
         
         
         // 往文件后方填入如下内容:
            export GRADLE_HOME=/media/ljc/dev/backup/gradle-5.3-all/gradle-5.3
			export PATH=${GRADLE_HOME}/bin:${PATH}

         // 此处"GRADLE_HOME="后方路径为个人复制的jdk文件夹地址,仅供参考
         // 检查无误后,按Esc键,进入退出模式
         // Shift+: 键,调出":"光标
         // 在":"后输入"wq"后回车(不想保存或重新编辑则输入"q!"之后回车)
         
            source /etc/profile (报错没有权限时前方加sudo)
            
            
  - 检查
  
    输入:    
        gradle -v 
        
        
      显示内容如下示例所示,表明安装成功:
      ------------------------------------------------------------
		Gradle 5.3
	  ------------------------------------------------------------

      Build time:   2019-03-20 11:03:29 UTC
      Revision:     f5c64796748a98efdbf6f99f44b6afe08492c2a0

      Kotlin:       1.3.21
      Groovy:       2.5.4
      Ant:          Apache Ant(TM) version 1.9.13 compiled on July 10 2018
      JVM:          11.0.2 (Oracle Corporation 11.0.2+9)
      OS:           Linux 5.0.0-33-generic amd64



	ps:本人已更新ubuntu budgie-19.04,所以内核版本为"Linux 5.0.0-33-generic",可忽略
        
        
        
#### Python(不感兴趣可忽略)
    系统自带有python,一般是python2,在终端中输入"python -V"即可查看版本,但是用于做Python3的深层次开发,功能不够,因此要安装Python3

    此外,使用 "sudo apt install python" 命令行安装来的python,功能不够完全.
    安装时默认不安装"tkhinter"等相关组件,导致部分GUI或需要调用的功能使用时会报错"No module named 'tkhinter'".
    而且即便手动从本地包安装后无法消除此类错误,因此这里采用本地包安装Python的方式安装Python.
    
 - 下载,地址:https://www.python.org/downloads/
 		进去点"DownLoad Python3.8"那个黄按钮,没毛病
        
        
 - 解压
 		为了防止编译器能够加载Python环境但pip没有权限安装包的问题,这里建议把Python包直接解压在下载的文件夹,
        或放在非root的文件夹中,且另外新建一个非root的文件夹做安装用
        解压命令和Java一致
        新建文件夹命令 
        mkdir /Python3.8
       
       
 - 安装(非root安装)
       
 		1. 检查openssl的环境.openssl是ubuntu上自带的一个可以远程的组件包,pip需要使用它相关的功能,因此需要对它进行检查
				
          终端输入:    
        
        	
            ssh -V
            
        返回信息:    
        
            OpenSSH_7.9p1 Ubuntu-10, OpenSSL 1.1.1b  26 Feb 2019
            
        此时说明是存在的.
        
        或终端输入:
        
            
            openssl version
            
            
       	此时返回信息是
        
      		OpenSSL 1.1.1b  26 Feb 2019
            
        同样也说明是存在openssl的.
        不存在的处理方法:
        
            sudo apt-get install openssl 
			sudo apt-get install libssl-dev 
            
            
         或
                     
         	yum install openssl-devel -y 
            
            '(个人不建议这种方式,因为使用Python3之后,依赖Python2的yum工具会因此在使用中报错" SyntaxError "导致不能使用)'
        
       	2. 安装过程
            用终端cd切换到Python包下载解压后的文件夹,或在该文件夹空白处右键菜单中点击"Open in Terminal"(此时是非root操作)
            
            ./configure --with-ssl --prefix=/mnt/software/Python3 
            
            "--with-ssl" : 这样防止pip不能使用ssl的问题出现
            "--prefix" : 安装到之前mkdir创建的非root文件夹内 
            	
      		make 
           
            (到此处不报错说明你很幸运了)
            
             make install 
            
            过程不报错完成后,查看一遍Python版本,如果是你安装的版本,恭喜你,你的安装过程基本完成了 
            
          3. 建立Python软连接
          
            cd /usr/bin
            
            ls -al python   查看当前Python指向的软连接
            
            ln -s /mnt/software/Python3  /usr/bin/python
            
            (ln -s python安装的文件夹 python连接的指向位置,个人理解,仅供参考)
            
            添加Python环境时,选中安装的文件夹下bin文件夹里的python3.8即可
            到这里,基本上Python的环境初步搭建好了
            
            编译器个人推荐Pycharm和Jupyter
            Pycharm 功能多适合正式开发,Jupter适合多环境下测试代码或者仅仅是普通功能
            https://jupyter.org/
          
          
#### NodeJs(前端用)
		
 - 安装
       
        node -v   检查当前版本
        
        
        sudo apt-get install nodejs
        
        sudo apt-get install npm
        
 - 问题处理        
      1. 开发时会遇到npm版本太老的情况,此时我们可以强行更新一波:
        
            sudo npm install npm -g
        
        或者"npm install –g n"更新到指定版本,如:
        
			npm install –g v10.16.0
        
      2. npm安装过程中会有很慢连不上外网镜像的情况,烦得一匹,这个时候我们可以用淘宝的镜像
      		npm get registry    获取当前的镜像地址
			
              https://registry.npmjs.org/

           设置为淘宝的镜像:
            npm config set registry http://registry.npm.taobao.org/
            
           设置回原镜像
			npm config set registry https://registry.npmjs.org/  
            
            
       3. 卡顿问题
       		选装cnpm.因为npm安装插件是从国外服务器下载，受网络影响大，可能出现异常，如果npm的服务器在中国就好了，所以我们乐于分享的淘宝团队干了这事
            
            npm install cnpm -g --registry=https://registry.npm.taobao.org
            
            安装完后一定要检查版本以防报错
            
            cnpm -v
            
   - 全局安装和本地安装
         
         npm install express          # 本地安装
        
         npm install express -g       # 全局安装
         
   - 卸载
        1. 先卸载 npm 
        
        
  		sudo npm uninstall npm -g
        
		
        2. 卸载nodejs
        
  		
          sudo apt-get remove nodejs
          
          

       
          
                 