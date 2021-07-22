# 赛昉7100开发板OH内核及init适配

## 运行init验证系统搭建流程

1.  赛昉7100开发板编译环境搭建
    完成以下步骤：[参考链接](https://wiki.seeedstudio.com/BeagleV-Make-File-System-Compile-uboot-Kernal/#compile-linux-kernel) 
    
    - 设置编译环境
    - 编译u-boot，得到u-boot.bin，u-boot.dtb
    - 编译OpenSBI, 得到fw_payload.bin
    - 烧录uboot
    - 编译Linux Kernel，得到Image.gz

2.  aosp-riscv环境搭建 
    [参考链接](https://github.com/T-head-Semi/aosp-riscv) 注意：推荐Ubuntu环境下编译，可用硬盘大小至少200G

3.  构建文件系统
    手动构建aosp-riscv rootfs
    ```
    cd aosp/out/target/product/generic_riscv64/
    cp -r root rootfs
    cp -r system rootfs/
    cp -r vendor rootfs/
    ```
    裁剪rootfs大小(避免uboot启动时解压失败)
    ```
    cd rootfs
    rm -r system/app/ system/fonts/ system/framework/ system/priv-app/ system/product/priv-app/ system/product/app/ system/product/media/
    ```
    打包文件系统
    ```
    find . | cpio -o -H newc | gzip > ../rootfs.cpio.gz
    ```

4.  将rootfs，kernel，uboot烧写至7100开发板，启动init
    [参考链接](https://wiki.seeedstudio.com/BeagleV-Make-File-System-Compile-uboot-Kernal/#compile-linux-kernel) 完成步骤：Move rootfs, kernel and uboot into BeagleV™ - Starlight

## 问题及解决

...

