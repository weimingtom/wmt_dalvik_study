# wmt_dalvik_study
My Android dalvik VM study (currently only dalvik for Android 2.2)  

## TODO, build Android src  
* 香橙派PCPlus和LCPI-H3的安卓4.4编译（需要迁移到VirtualBox）  
三星开发板的安卓4.4编译（可能缺少一些工具的编译指引，见weibo）  
古老三星版开发板的安卓2.3编译（参考大SD卡的内容，上传网盘？）  

* 我恐怕需要找时间整理编译和运行旧版本安卓（安卓2.3和安卓4.4和安卓5）的指引记录备忘文档——老掉牙安卓，怀旧用（划去，研究dalvik用），部分未尝试  
（1）mini210（s5pv210）的安卓2.3，或者用s3c的arm11也支持安卓2.3 (s3c6410???)    
（2）香橙派PC Plus和LCPI-H3的安卓4.4  
（3）NanoPC-T2（S5P4418）的安卓5  

* 注意香橙派PC Plus买了  

* My weibo digest, s3c arm11==s3c6410 (?)        
```
我找到飞凌的开发板，可以运行旧版本的android 2.3（应该只此一家了）——
除了我之前购买的友善之臂的nanopc-t2可以运行android5和android4
（我实际测试过可以编译刷写运行android 5的源代码），
我发现飞凌有2种开发板也可以：
飞凌的S5P4418（OK4418）也可以运行android 5，
价格跟nanopc-t2差不多，也是400左右，板载功能更多，
支持hdmi，但缺点是下载资料需要购买板之后才能拿到；
另外飞凌的S3C6410（OK6410）支持android 2，
价格在600元左右，下载资料是网盘公开的。
我打算买OK6410B（无核心板）+4.3寸屏，
不过可能要研究好它的android 2.3源代码再考虑购买。
其实友善之臂以前也有6410的板（现在没货了），
不过友善之臂官方没有提供android源代码编译的支持服务，
但飞凌提供了
```
```
目前为止，我知道能运行安卓2的开发板：
（1）s3c arm11
（2）s5pv210
（3）MYS-SAM9G45
（4）AT91SAM9X35
（5）cubieboard1，全志A10 ​​​
```
```
buildroot好像已经支持x11了，我看到有人写了s3c arm11（虽然不是友善的板），
如何编译运行x11，应该是buildroot的非正式的s3c移植版
（真正的buildroot好像是没有s3c和s5p的支持）：
blog.csdn.net/u011011827/article/details/115728941 ​​​
```
```
买了块mini210s，试过很好用，打算以后主要用这个而不用s3c arm11了。
mini210s（s5pv210）和s3c arm11的区别是：
（1）Win CE和安卓略有不同，210的固件要大一些，加入一些apk
（2）210的调试串口(con1)是6线，不过可以兼容s3c arm11的四线插头(con1)，
方法是空出右面两针（靠近开关那边）
（3）210的开关ON/OFF方向是反过来的
（4）210支持mini-hdmi，不过我没测试过
（5）210的安卓很流畅，接近于手机效果，而s3c arm11有明显的卡顿
(6) 210需要tf卡而非s3c arm11的SD大卡，我试过用非闪迪的tf卡都可以烧录，
而s3c arm11可能只能用闪迪的SD卡。总体来说mini210s要更适合用来研究安卓2.3，
出问题的概率比较低，不过着两个板都似乎有点电源不足（屏幕容易挂）
```
```
现在我第三块s3c arm11板可以偶尔能跑得动Android 2.3了——之所以说偶尔，
是因为有一定概率会出现无法响应的对话框然后直接挂掉，
或者看到频繁地移动焦点然后卡住在桌面。
我试过可以用鼠标控制（可能要在开机前装好USB鼠标），
如果用鼠标，256M内存鼠标移动的图标会有点卡顿，
而且右键会执行后退操作，滚轮是向上向下移动焦点，
方便不需要滚动页面（因为卡顿，滚动会很容易误操作为点击）
```
```
我又搞了一块（第三块）s3c arm11的256M内存版，
结果这个居然也是无法运行Android 2.3的
（和之前的128M内存版类似），
运行Linux也会可能crash，
看来这些s3c的散货很大概率会出问题
（估计是用于正式用途的问题板换下来的），
除非只是运行Linux，不过比较便宜，
买来权当实物纪念的古董。。。
```
```
其实从友善的论坛记录，s3c arm11以前甚至是有安卓2.2的移植
（当时应该是2011年），只不过现在已经很难找到当时的文件，
而我只能拿到安卓2.3.4（实际上应该还有安卓2.3.2），
可惜这些东西没有保留下来。
另外当时应该还有很多家是做这个核心板的，
有些是移植安卓2.1，如今觉得很好用，
但当时是非常高昂的成本
```
```
我通过钞能力搞到第二块s3c arm11，256M内存，
终于可以跑起来android 2.3.4。
另外我找了个其他牌子的SD大卡，
发现还是没办法烧写s3c arm11，
看来只有SanDisk才行，我试过32GB可以用 ​​​
```
```
我也成功编译出mini210(s5pv210)的android 2.3.1的根文件系统，方法和s3c arm11差不多，
如果可以编译出s3c arm11的Android 2.3.4，这个也会很容易
（使用ubuntu 12，32位，安装的apt包相同，gcc4），
只需要改几个文件，一个mk文件（-Wno-error）和
genrootfs.sh（开头的/bin/sh改成bash）。
至于Linux的zImage编译，我用了相同的工具链，
按道理是和s3c arm11是通用的（文件名的版本相同但时间不同）。
因为还没买210的开发板，等以后买到手再测试效果
```
```
除了我上次说的那个s3c arm11，我发现还有s5pv210（mini210s）也是支持Android 2.3的，
只不过这个是A8架构，而且其实是支持Android 4.0.3
（不过光盘里面也提供了2.3的根文件系统源码）。
s3c arm11和s5pv210的区别是210支持mini-hdmi输出，
不过不提供u-boot代码（可能已经集成在闭源的SD卡bootloader中）
```
```
另外，s3c arm11还有一些好处，我是比较喜欢的，例如支持分线器（集线器）接键盘鼠标，
这样就可以不需要用笔点电阻触摸屏了。另外可以接卡套接tf卡，用于文件复制，
这样可以省了网线传文件的麻烦（可能usb host也可以接u盘，待考），
虽然卡套无法用于卡刷固件（这个板的最原始的bootloader似乎不支持卡套，
我是用32G的相机SD卡）
```
```
总体来说，我觉得这个古老的s3c arm11的可玩要远大于imx283和现在的很多带屏板
（例如ssd202d和全志d1、v3s、f1c之类），
虽然内存小和主频低（其实现在很多带屏板的内存也只有128）。
主要是支持的OS很多（古老的Win CE6），
甚至还能bare-metal和ucos2（虽然需要一些闭源工具）。
我打算过一段时间再买一个，看能否买到256M版的
```
研究了半天，终于理解了友善之臂s3c arm11开发板的简单用法：
首先，如果要卡刷（友善的闭源bootloader），
需要大的SD卡，我试过卡套果然是不行。然后，板上的PC串口线用不了，
我是用四线串口线去看调试输出和命令行（友善的linux是用busybox）。
然后，我没跑起来Android 2.3，似乎是因为内存不够（我买了128M内存版，
可能要再买一个256M版才行，待考）。最后，这板支持四种系统，
友善linux（qtopia）、Android 2.3.4、Windows CE和xubuntu，
其中Android是开源的（打包器可能不开源），CE闭源，
xubuntu的根文件系统闭源，友善linux似乎提供了一个busybox的
最小化的根文件系统和qt和闭源文件系统。
应该是可以看到framebuffer设备的，问题是可能会被占用，待考
```
我现在怀疑我需要迁移到dalvik的Android 4.4版本而不是去研究Android 2.3，
原因是，我发现能找到的支持Android 2.3的开发板就只剩下s3c的arm11开发板，
因为到了Android 4的armv7a就是不支持arm11，
而大部分开发板除了arm9和arm11以外，就是arm v7a和以上的架构了。
所以事实上，开发板最低支持的Android版本是4，而且考虑到内存问题，
1G内存才比较够用，arm11的256M似乎有点不太够
```
```
最近入手了新的开发板，s3c的arm11开发板（跟2440很像，只不过不是arm9，PCB也很类似于2440），
我主要是想研究Android代码，因为它有一份Android 2.3的移植代码
（我上次说过那个很像buildroot的编译过程，只需要编译成根文件系统）。
令我惊讶的是这板是新的，可能有PCB图纸可以打印出来 ​​​
```
我以前对有些开发板用buildroot只用于生成根文件系统（linux内核另外生成）感觉很不解，
不过最近发现android似乎也可以这样做（我是研究s3c arm11开发板的android 2.3）——
简单来说诸如dalvikvm原生程序的生成和文件系统打包非常类似于buildroot，
也可以最终输出到img文件或者对应的文件（ext4文件系统），
至于内核和bootloader则分开编译，与android的构建可以无关
```

## TODO  
* https://github.com/kai4785/webos_dalvik  

## work  
* (cygwin failed), https://github.com/weimingtom/dalvik_cygwin_port  
* (cygwin failed), dalvik_v1.7z, dalvik_v4.7z  
* (cygwin failed), dalvik_cygwin_port-master_20180801_v2.rar  
* rpd 2017 (raspbian x86, debian 9) run success, dalvik_linux_port_v10_success.tar.gz  

## 2022-02-19, dalvik_linux_port_v10_success.tar.gz  
(1) must use debian/linux 32bit, (64 bit failed) , use rpd 2017 run success  
(2) see Makefile, sudo apt install  
sudo apt install libffi-dev  
sudo apt install libicu-dev  
sudo apt install libsqlite3-dev  
sudo apt install libssl-dev  
sudo apt install libexpat-dev  
(3) make clean all  
(4) run testvm/prepare_jar.txt  
$ make clean all  
$ sudo mkdir -p /data/dalvik-cache  
$ sudo chown -R pi:pi /data  
$ sudo mkdir -p /system/bin  
$ sudo chown -R pi:pi /system  
$ cp dalvik/dexopt/dexopt /system/bin/.  
$ cp testvm/foo.jar /data/.  
$ cp testvm/framework2/*.jar /data/.  
$ cd dalvik/dalvikvm  
$ make test  
./dalvikvm -Xbootclasspath:/data/core.jar -classpath /data/foo.jar Foo  
only foo.jar and core.jar need  
(5) if gdb, see   
make debug  
if debug multi processes(dexopt and dalvikvm)  
(gdb) set follow-fork-mode child  
(gdb) set detach-on-fork on  
(gdb) b dvmAbort  
(gdb) r  

## Chun-Yu Wang's dalvik, WJY's Simple Dalvik Virtual Machine  
* https://github.com/wicanr2/simple_jvm_and_dvm  
* https://github.com/majestyhao/SimpleDalvik  
* https://github.com/jserv/simple-dvm  
* https://github.com/cycheng/simple-dvm  

## android-dalvik-vm-on-java  
To study the concept and architecture of Dalvik VM,   
Koji Hisano is developing this for J2ME CLDC environments as   
on-going research at "eflow Inc."  
* https://code.google.com/archive/p/android-dalvik-vm-on-java/  
* https://github.com/weimingtom/android-dalvik-vm-on-java  

## etc  
* https://github.com/jjfiv/dalvik-js  
* https://github.com/MiCode/dalvik  
* https://github.com/lexrrx/DalvikVM-Servlet  

## REDasm  
* https://redasm.io  

## Porting Dalvik  
* https://wladimir-tm4pda.github.io/porting/dalvik.html#dalvikInterpreter  

## port  
* https://stackoverflow.com/questions/3542268/how-can-i-compile-dalvik-to-run-it-locally-on-linux  
* https://github.com/reyammer/dexware  
* https://code.google.com/archive/p/dvk/  

## some books  
* search baidupan, dalvik_book  

## (IMP?) 忘记哪里记录 NanoPC的打包工具，待考  
* sd-fuse_h3， search百度盘 sd_update
* https://github.com/friendlyarm/sd-fuse_h3
* https://github.com/friendlyarm/sd-fuse_s5p4418  
* make_ext4fs, 友善之臂FriendlyArm, NanoPC-T2, S5P4418, Android 5.1 build ???  
* https://github.com/weimingtom/wmt_ai_study/blob/master/weibo_001.txt  
* https://github.com/woju/make_ext4fs  
* (dead) https://github.com/rendiix/android-prebuilt-binary-tools  
* https://github.com/arfoll/updater-hack  
* https://github.com/weihutaisui/BCM/tree/master/HGU_BCM68580/02_src_502L04patch2/hostTools/make_ext4fs/extras_latest/extras/ext4_utils  
* https://wiki.friendlyelec.com/wiki/index.php/NanoPC-T2    
* https://wiki.friendlyelec.com/wiki/index.php/NanoPC-T3  
