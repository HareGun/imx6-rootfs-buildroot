### 用buildroot构建的根文件系统

未上传/output，编译后需修改busybox配置和libbb文件后重新编译busybox和rootfs



### 步骤

1. 先编译一次

   ```
   make
   ```

2. 对busybox进行修改

   把/libbb里面两个.c替换掉（如果不需要中文支持可不换）

   把busybox_config替换掉.config

3. 在buildroot目录下重新编译busybox

   ```
   make busybox-menuconfig
   make busybox
   ```

4. 重新编译rootfs

   ```
   make
   ```

5. 添加wilist工具（如不需要可不添加）

   在wilist源码目录下编译wilist（默认已编好，arm32版本的）

   ```
   make clean
   make
   ```

   编译完成以后就会在当前目录下生成 iwlist、iwconfig、iwspy、iwpriv、ifrename 这 5 个工
   具，还有 libiw.so.29 这个库文件。

   将这 5 个工具拷贝到开发板根文件系统下的/usr/bin 目录中，

   将 libiw.so.29 这个库文件拷贝到开发板根文件系统下的/usr/lib 目录中