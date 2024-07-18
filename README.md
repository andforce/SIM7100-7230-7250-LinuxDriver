## 驱动安装详细步骤

1. 把 SIM7100CE 通过 USB 插入安装了Linux的PC或者树莓派
   ![image](https://github.com/user-attachments/assets/f705c9f0-4e38-4a19-81a2-9272930310f0)
2. 执行 `lsusb`,查找 vid:pid 是 1e0e:9001 的USB设备
   ![image](https://github.com/user-attachments/assets/e77ce146-f707-4b23-a409-4d219bd3bee4)
3. 执行`“sudo rmmod usbserial`命令移除usb串口设备，这时候会报错，直接忽略就行
4. 编译GobiSerial.c
   ```shell
   $ make
   rm -rf *.o *~ core .depend .*.cmd *.ko *.mod.c .tmp_versions Module.* modules.order
   make -C /lib/modules/6.6.31+rpt-rpi-v8/build M=/home/dy/code/SIM7100-7230-7250-LinuxDriver modules
   make[1]: Entering directory '/usr/src/linux-headers-6.6.31+rpt-rpi-v8'
   CC [M]  /home/dy/code/SIM7100-7230-7250-LinuxDriver/GobiSerial.o
   /home/dy/code/SIM7100-7230-7250-LinuxDriver/GobiSerial.c:630:12: warning: ‘GobiSuspend’ defined but not used [-Wunused-function]
   630 | static int GobiSuspend(
      |            ^~~~~~~~~~~
   MODPOST /home/dy/code/SIM7100-7230-7250-LinuxDriver/Module.symvers
   CC [M]  /home/dy/code/SIM7100-7230-7250-LinuxDriver/GobiSerial.mod.o
   LD [M]  /home/dy/code/SIM7100-7230-7250-LinuxDriver/GobiSerial.ko
   make[1]: Leaving directory '/usr/src/linux-headers-6.6.31+rpt-rpi-v8'
   
   ```
   如果能生成 `GobiSerial.ko` 这个文件，就表示成功编译了，忽略警告信息就行
5. 启用驱动`sudo modprobe usbserial && sudo insmod GobiSerial.ko`
   ```shell
   $ sudo modprobe usbserial && sudo insmod GobiSerial.ko
   ```
   如果能看到6个USB串口表示驱动安装成功：
   ![image](https://github.com/user-attachments/assets/4959b7d6-754e-42e1-a6e3-d890108d71e8)

## 各个串口的作用
Notes: there are 6 ports for SIM7100 modules in Linux host.
1) /dev/ttyUSB0 : diag port for output developing messages
2) /dev/ttyUSB1 : NMEA port for GPS NMEA data output
3) /dev/ttyUSB2 : AT port for AT commands
4) /dev/ttyUSB3 : Modem port for ppp-dial
5) /dev/ttyUSB4 : audio port
6) /dev/ttyUSB5 : Virtual Net card

## SIMCOM7系列PCM情况
SIM7000x	✅

SIM7020	❌

SIM7060G	国内没有卖的，不考虑

SIM7100E	✅ AT+CPCMREG 文档中有

SIM7500A	✅ AT+CPCMREG 文档中有

SIM7500E	✅ AT+CPCMREG 文档中有

SIM7600C	✅ AT+CPCMREG 文档中有

SIM7600E	✅ AT+CPCMREG 文档中有

SIM A7670E ✅ AT+CPCMREG 文档中有


驱动文件来源：https://simcom.ee/documents/?dir=SIM7100E/Driver/Linux

SIMCOM各系列模块的文档列表：https://simcom.ee/documents/
