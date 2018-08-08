## root方法
### 安装twrp
* 下载https://twrp.me/
* 选择device：https://twrp.me/Devices/

#### twrp加载（注意 去掉锁屏信息）
* 加载twrp：fastboot boot 下载路径/twrp.img

#### 刷入twrp（不靠谱）
* adb reboot bootloader
* 刷入twrp：fastboot flash recovery 下载路径/twrp.img
* fastboot reboot 

### 安装Magisk
下载https://magiskmanager.com/

### 刷入magisk
adb reboot bootloader
fastboot boot 下载路径/twrp.img
twrp中选择install magisk.zip
