# README

This guide provides instructions for compiling the Linux kernel and updating it on a Raspberry Pi SD card.

## 1. Modify the Compiler Path

Before compiling the kernel, you need to update the `set_compiler.sh` file with the correct path to your cross-compiler. Open the file `navio2-4.19.127-rt/set_compiler.sh` and modify the following line:

```
export PATH=/path/to/gcc-linaro-7.5.0-2019.12-x86_64_aarch64-linux-gnu/bin:$PATH
```
Replace `/path/to/gcc-linaro-7.5.0-2019.12-x86_64_aarch64-linux-gnu/bin` with the actual path to your cross-compiler.

## 2. Compiling the Kernel
To compile the kernel, follow these steps:
```
source set_compiler.sh
make ARCH_CFLAGS=-w bcm2709_navio2_defconfig
make Image modules dtbs -j8
```

## 3. Updating the Kernel on the Raspberry Pi SD Card
After compiling the kernel, you need to copy the necessary files to the Raspberry Pi SD card. Replace [ubuntu username] with your actual Ubuntu username.

```
sudo cp ./arch/arm64/boot/Image /media/[ubuntu username]/boot/kernel8.img
sudo cp ./arch/arm64/boot/dts/overlays/*.dtb* /media/[ubuntu username]/boot/overlays/
sudo cp ./arch/arm64/boot/dts/overlays/README /media/[ubuntu username]/boot/overlays/
sudo make INSTALL_MOD_PATH=/media/[ubuntu username]/rootfs modules_install
```
