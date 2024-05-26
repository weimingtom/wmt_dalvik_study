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

* my weibo digest  
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
