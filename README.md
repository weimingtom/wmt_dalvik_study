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
我找到飞凌的开发板，可以运行旧版本的android 2.3（应该只此一家了）——除了我之前购买的友善之臂的nanopc-t2可以运行android5和android4（我实际测试过可以编译刷写运行android 5的源代码），我发现飞凌有2种开发板也可以：飞凌的S5P4418（OK4418）也可以运行android 5，价格跟nanopc-t2差不多，也是400左右，板载功能更多，支持hdmi，但缺点是下载资料需要购买板之后才能拿到；另外飞凌的S3C6410（OK6410）支持android 2，价格在600元左右，下载资料是网盘公开的。我打算买OK6410B（无核心板）+4.3寸屏，不过可能要研究好它的android 2.3源代码再考虑购买。其实友善之臂以前也有6410的板（现在没货了），不过友善之臂官方没有提供android源代码编译的支持服务，但飞凌提供了
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
