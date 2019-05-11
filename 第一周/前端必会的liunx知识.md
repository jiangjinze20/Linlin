##  一、认识linux

#### 1.学习liunx的必要性： 
      （1）. 绝大多数服务器的环境都是在linux下开发的，较少的比如C#，或者公司技术能力不行的
      （2）. 许多发开环境需要在linux下 ---自动化发布、脚本的依赖   
      （3）. 常用的几十个命令需要识记（英文缩写）-> 命令有意义的英文change dir cd  /  ls list
 
#### 2.linux的官网：https：//www.kernel.org 
 
    操作系统的内核   源代码程语言写的（算法、流程）[底层效率，频繁，提供API][业务层效率要求较低，不频繁]
    其他的是发型版本，加入了很多自己的外壳。
 
#### 3.linux 与windows的区别：
 
     1.  99.9%用于服务器
     2.  ulinx较为古老，制定些规范
     3. 微软子系统、发布终端拥抱linux
     4.图形界面系统资源的消耗，可以不装图形界面，减少性能损耗
     5.不能把性能的习惯放在加硬件上，是有天花板的，inter最近发布的处理器多核心方向发展，
       提高主频已经不行了，接近物理极限，在提高会遇见神秘的现象量子碎穿现象
     6.内核的区别：以简为美 
     7.mac的内核是BSD[有版权]
     8.发展历程可以自己扩展下
     9.linux是归贝尔实验室 AT&T
 
## 二、安装vmware
 
    下载安装 vmware workstation pro  /  MAC装fusion / 国外网站慢可在360商店下载
    ⽹址：https://www.vmware.com/cn.html  
    ⾸先要 vmware.com 注册⼀个⽤户
    到下载⻚⾯下载 VMware Workstation Pro 15.0.2 for Win
    下载⻚⾯链接https://my.vmware.com/cn/web/vmware/iputing/vmware_workstation_pro/15_0
    把 vmware workstation pro 安装到你的windows电脑上 
    
     
    
                处理器 核心数量 2 2  
                1.磁盘大小的坑
                  1.立即占用20G的物理磁盘
                  2.单个文件性能高点
                  3.多个文件在拷贝时速度快点，底层io设备特点决定[一般不会动]
                
              下载安装 vmware workstation pro
              ⽹址：https://www.vmware.com/cn.html
              ⾸先要 vmware.com 注册⼀个⽤户
              到下载⻚⾯下载 VMware Workstation Pro 15.0.2 for Win下载⻚⾯链接https://my.vmware.com/cn/web/vmware/inputing/vmware_workstation_pro/15_0
              把 vmware workstation pro 安装到你的windows电脑上
              
              
              
              第二行会测试磁盘内存在安装没必要，选择第一行
              
   下载 CentOS 安装盘镜像
      CentOS官⽹： https://www.centos.org/
      光盘镜像下载⻚⾯：https://www.centos.org/download/
      点击“DVD ISO”按钮，这个是带有图形界⾯的版本。Minimal ISO 不带图形界⾯，最好也下
      载，我们以后的课程中会⽤到。
      点击按钮后会进⼊⼀个镜像⽹站的列表，选择阿⾥云、华为云、163等⽐较快的服务器
      
      开启计算机硬件的虚拟化⽀持选项
          先打开任务管理器，切换到“” 标签⻚，检查“虚拟化”是否为已启⽤状态[不支持你启动系统会报错]
          
         开启计算机硬件的虚拟化⽀持选项  --主板较老会出现的问题
先打开任务管理器，切换到“” 标签⻚，检查“虚拟化”是否为已启⽤状态 
          
          如果状态为“未启⽤”，按照如下步骤操作
      1、重启电脑，在主板显示画⾯，快速寻找进⼊BIOS的按键。根据品牌不同，可能是F2、Del
      或其他键。 2、进⼊BIOS后，寻找进⼊“System Configuration”。 3、找到“Virtualization
      Technology”，按回⻋键。 4、选择“Enabled”，按Enter回⻋键。 5、然后保存重启即可
          
          
          cmder增强行终端
          微软发布的terminal  可以去microsft git 看源码  xshell  putty
          
          https：//cmder.net  完整版有许多内置
          
⽬录 应放置档案内容
/bin
系统有很多放置执⾏档的⽬录，但/bin⽐较特殊。因为/bin放置的是在单⼈维护模式下
还能够被操作的指令。在/bin底下的指令可以被root与⼀般帐号所使⽤，主要有：
cat,chmod(修改权限), chown, date, mv, mkdir, cp, bash等等常⽤的指令。
/boot
主要放置开机会使⽤到的档案，包括Linux核⼼档案以及开机选单与开机所需设定档等
等。Linux kernel常⽤的档名为：vmlinuz ，如果使⽤的是grub这个开机管理程式，则
还会存在/boot/grub/这个⽬录。
/dev
在Linux系统上，任何装置与周边设备都是以档案的型态存在于这个⽬录当中。 只要通
过存取这个⽬录下的某个档案，就等于存取某个装置。⽐要重要的档案有/dev/null,
/dev/zero, /dev/tty , /dev/lp, / dev/hd, /dev/sd*等等
/etc
系统主要的设定档⼏乎都放置在这个⽬录内，例如⼈员的帐号密码档、各种服务的启
始档等等。 ⼀般来说，这个⽬录下的各档案属性是可以让⼀般使⽤者查阅的，但是只
有root有权⼒修改。 FHS建议不要放置可执⾏档(binary)在这个⽬录中。 ⽐较重要的档
案有：/etc/inittab, /etc/init.d/, /etc/modprobe.conf, /etc/X11/, /etc/fstab,
/etc/sysconfig/等等。 另外，其下重要的⽬录有：/etc/init.d/ ：所有服务的预设启动
script都是放在这⾥的，例如要启动或者关闭iptables的话： /etc/init.d/iptables
start、/etc/init.d/ iptables stop/etc/xinetd.d/ ：这就是所谓的super daemon管理的
各项服务的设定档⽬录。/etc/X11/ ：与X Window有关的各种设定档都在这⾥，尤其
是xorg.conf或XF86Config这两个X Server的设定档。
/home
这是系统预设的使⽤者家⽬录(home directory)。 在你新增⼀个⼀般使⽤者帐号时，
预设的使⽤者家⽬录都会规范到这⾥来。⽐较重要的是，家⽬录有两种代号： ~ ：代
表当前使⽤者的家⽬录，⽽ ~guest：则代表⽤户名为guest的家⽬录。
系统的函式库⾮常的多，⽽/lib放置的则是在开机时会⽤到的函式库，以及在/bin
或/sbin底下的指令会呼叫的函式库⽽已 。 什么是函式库呢？妳可以将他想成是外挂，
如果状态为“未启⽤”，按照如下步骤操作
1、重启电脑，在主板显示画⾯，快速寻找进⼊BIOS的按键。根据品牌不同，可能是F2、Del
或其他键。 2、进⼊BIOS后，寻找进⼊“System Configuration”。 3、找到“Virtualization
Technology”，按回⻋键。 4、选择“Enabled”，按Enter回⻋键。 5、然后保存重启即可。


终端的基本使用

ssh root@ ip address 139.224.236.30  密码不回显

退出exit

看ip地址 ifconfig 古老的
ip addr 组合命令
The authenticity of host '192.168.1.105 (192.168.1.105)' can't be established.
RSA key fingerprint is SHA256:zsjSGLnHvjOOxFBCs+B9LnJ1CZoLC+hLl2g2Ug03YrI. 
Are you sure you want to continue connecting (yes/no)?  第一次登陆需要继续吗 / 防止伪造服务器


数据安全(做好备份)、  环境安全  

windows 代码怎么传上去ftp
scp 命令远程拷贝

没有ip说明网卡配置有问题 --是否选用桥接  --是否开启网络
scp ./index.html root@192.168.1.105:/root

目录树的结构：
认识目录

接u盘要瓜子啊mount

bin shell 不能被内置的命令
etc配置文件
第一个是本地回环地址  第二个是物理网卡地址 那不到ip地址怎么排查
1.虚拟机配置是不是桥接
2.物理机网卡是不是激活
3.是你没有激活linux的网卡，我们只能在配置文件手动激活
      
      cd -> etc ->cd sysconfig ->cd network-scripts
      cat ifcfg-eth0（网卡名字）
       修改 ONBOOT yes
       停止网卡 ifdown eth0
      ifup eth0 启动网卡
      
      vi的简单使用行编辑命令
       进入时只读状态 按下i[下面显示insert]
       esc
       :wq  写、退出 ！是强行退出：q！ 不保存退出
       nano 要自己安装 有点图形界面
       yum  更新软件仓库索引  
       yum install nano
       是不是继续？ y  指纹秘钥y 安装ok
    
    上尖符号是ctrl
    nano不是正统的东西
    root 超级管理员的家
    home 普通人员的家
    ~ 是代表当前用户的home（家）
    
    boot 核心文件不要动 【启动文件和内核文件】
    
    centos 进入单用户模式pwd 忘记密码

    
    安装nodejs
    1.必须加源官方仓库没有
    
    
    端口： 开门 
    linux看服务systemctl
    
    查看服务状态 systemctl status nginx
    
    systemctl [启动 暂停 服务状态]  start stop status restart重启  reload 热更新配置
    
    pm2维护node 的程序单线程的 多任务 nohub很大的日志文件 setsid 
    
    rm 文件  -r
    rm -r dir mac
