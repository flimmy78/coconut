Can contact me with Email emblinuxedu@163.com  OR +86-13871114284

==================================================================
拿到开发板请先进入到linux系统里面，用户root.密码无.
用comport工具测试一下GPRS/WIFI等是不是正常，至少我在出货前测试都OK.
前面板从右往左第三个灯为GPRS状态灯，闪烁状态表示模块已经启动，AT就OK
comport -ioctl /dev/gprs 1 1       ## power on  2G
comport -ioctl /dev/gprs 2 1       ## power off 2G
comport -d /dev/ttyS2              ## 2G AT test
comport -ioctl /dev/ttyUC864E1 2 1 ## power on  3G   
comport -ioctl /dev/ttyUC864E1 2 1 ## power off 3G   
comport -d /dev/ttyUSB0            ## 3G AT test
加上WIFI驱动后用ifconfig -a你可以看到ra0设备，说明WIFI硬件OK


==================================================================
如果你不是高手，请不要尝试重新烧录UBOOT，因为你有可能使开发板成为砖,
虽然我不害怕砖头，但是板子毕竟现在不在我这，所以，请尽量先不要刷uboot

硬件V21/2烧录的固件为 2.6.22-LHG-uImage_2014 AND 2.6.22-LHG_rootfs_2014
硬件V23  烧录的固件为 2.6.22-STD-uImage_2014 AND 2.6.22-NO6_rootfs_2014
这两硬件我烧录的是不同的uboot,区别是mkimage不同，此工具从uboot中获取，
在编译kernel是一定要用到这个工具，而在制作rootfs时不一定需要此工具

制作 硬件V21/2的版本我烧录的固件为请参见 ../doc/ForV22_LHG_Version.html 
制作 硬件V23  的版本我烧录的固件为请参见 ../doc/ForV23_LHG_Version.html
测试 硬件V21/2的版本详细过程请参见       ../doc/CMD_Guide_LHG_V22.html
测试 硬件V23  的版本详细过程请参见       ../doc/CMD_Guide_STD_V23.html


==================================================================
############## 在当前uboot中调试新的文件系统和内核文件 ############
set serverip 192.168.1.1;set ipaddr 192.168.1.2;set ethaddr 00:00:21:0c:2d:1a

----------------- For V23 STD Version ----------------------------
tftp 20000000 2.6.22-STD-uImage_2014  # 从192.168.200.138下载内核文件
tftp 21100000 2.6.22-NO6_rootfs_2014  # 从192.168.200.138下载rootfs

----------------- For V21/2 LHG Version ----------------------------
tftp 20000000 2.6.22-LHG-uImage_2014  # 从192.168.200.138下载内核文件
tftp 21100000 2.6.22-LHG_rootfs_2014  # 从192.168.200.138下载rootfs

bootm 20000000                        # 从内存启动内核
