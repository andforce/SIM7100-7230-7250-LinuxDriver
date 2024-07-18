1. 把 SIM7100CE 通过 USB 插入安装了Linux的PC或者树莓派
   ![image](https://github.com/user-attachments/assets/f705c9f0-4e38-4a19-81a2-9272930310f0)
2. 执行 `lsusb`,查找 vid:pid 是 1e0e:9001 的USB设备
   ![image](https://github.com/user-attachments/assets/e77ce146-f707-4b23-a409-4d219bd3bee4)
3. 执行`“sudo rmmod usbserial`命令移除usb串口设备，这时候会报错，直接忽略就行
4. 编译GobiSerial.c
   ```shell
      make
   ```
   
文档：

https://simcom.ee/documents/

文件来源：

https://simcom.ee/documents/?dir=SIM7100E/Driver/Linux
