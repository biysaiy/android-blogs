### 配置代码环境
- AOSP源码地址：https://mirrors.tuna.tsinghua.edu.cn/help/AOSP/
- 指定master分支版本
```
repo init -u https://aosp.tuna.tsinghua.edu.cn/platform/manifest -b master
```

### veridex的编译方法
首先需要建立好AOSP的构建环境，可以使用macOS或者Ubuntu，这里以64位的Ubuntu 16.04.4 LTS为例：

- 安装OpenJDK 8，命令：sudo apt install openjdk-8-jdk

- 安装依赖的库和组件，命令：sudo apt-get install git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev libgl1-mesa-dev libxml2-utils xsltproc unzip

- 进入AOSP根目录 make appcompat -j32
```
============================================
PLATFORM_VERSION_CODENAME=Q
PLATFORM_VERSION=Q
TARGET_PRODUCT=aosp_arm
TARGET_BUILD_VARIANT=eng
TARGET_BUILD_TYPE=release
TARGET_ARCH=arm
TARGET_ARCH_VARIANT=armv7-a
TARGET_CPU_VARIANT=generic
HOST_ARCH=x86_64
HOST_2ND_ARCH=x86

.....

DroidDoc took 11 sec. to write docs to out/soong/.intermediates/frameworks/base/hiddenapi-lists/android_common/docs/out
javadoc: option --boot-class-path not allowed with target 1.9
[100% 2601/2601] build out/target/common/obj/PACKAGING/hiddenapi-blacklist.txt
```
可以看到在out/target/common/obj/PACKAGING/目录下，生成了三个隐藏API的列表文件**hiddenapi-blacklist.txt（黑名单）、hiddenapi-dark-greylist.txt（暗灰名单）、hiddenapi-light-greylist.txt（亮灰名单）**，这些即为ART检查API调用情况的依据

### veridex检测方式
Build一个测试用的APK以后，进入到AOSP源码的根目录下（必须在AOSP源码根目录下），执行以下命令
```
./art/tools/veridex/appcompat.sh --dex-file=[待检测apk的路径]  --imprecise（这个参数可选，建议加上，更准确）
```

