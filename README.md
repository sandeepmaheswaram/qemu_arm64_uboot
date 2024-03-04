# qemu_arm64_uboot
git clone https://github.com/u-boot/u-boot.git -b v2022.07

make qemu_arm64_defconfig

make

On Buildroot select bootloaders->uboot->qemu_arm64 


Follow the link https://schspa.tk/2019/10/22/uboot-online-debug.html

(gdb) p/x ((gd_t *)$x18)->relocaddr

$8 = 0x7ff12000

(gdb) add-symbol-file u-boot $8
