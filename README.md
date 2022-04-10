# wmt_dalvik_study
My Android dalvik VM study (currently only dalvik for Android 2.2)  

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
