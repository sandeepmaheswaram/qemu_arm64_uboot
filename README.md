# qemu_arm64_uboot
git clone https://github.com/u-boot/u-boot.git -b v2022.07

make qemu_arm64_defconfig

make

On Buildroot select bootloaders->uboot->qemu_arm64 
