# How to build
- source openembedded-core/oe-init-build-env
- cp bblayers.conf to build/conf
- cd build && MACHINE=qemuriscv64 bitbake core-image-full-cmdline/core-image-minimal

# Output

ls tmp-glibc/deploy/images/qemuriscv64

# Run Qemu
```
free@free:~/yocto/riscv-yocto/build$ runqemu qemuriscv64
 runqemu qemuriscv64
runqemu - INFO - Running MACHINE=qemuriscv64 bitbake -e ...
runqemu - INFO - Continuing with the following parameters:
KERNEL: [/home/free/yocto/riscv-yocto/build/tmp-glibc/deploy/images/qemuriscv64/Image--5.15.38+git0+37891dc371_cc9695f5fd-r0-qemuriscv64-20220612021452.bin]
BIOS: [/home/free/yocto/riscv-yocto/build/tmp-glibc/deploy/images/qemuriscv64/fw_jump.elf]
MACHINE: [qemuriscv64]
FSTYPE: [ext4]
ROOTFS: [/home/free/yocto/riscv-yocto/build/tmp-glibc/deploy/images/qemuriscv64/core-image-full-cmdline-qemuriscv64-20220612021452.rootfs.ext4]
CONFFILE: [/home/free/yocto/riscv-yocto/build/tmp-glibc/deploy/images/qemuriscv64/core-image-full-cmdline-qemuriscv64-20220612021452.qemuboot.conf]

runqemu - INFO - Setting up tap interface under sudo
runqemu - INFO - Network configuration: ip=192.168.7.2::192.168.7.1:255.255.255.0::eth0:off:8.8.8.8
runqemu - INFO - Running /home/free/yocto/riscv-yocto/build/tmp-glibc/work/x86_64-linux/qemu-helper-native/1.0-r1/recipe-sysroot-native/usr/bin/qemu-system-riscv64 -device virtio-net-device,netdev=net0,mac=52:54:00:12:34:02 -netdev tap,id=net0,ifname=tap0,script=no,downscript=no -object rng-random,filename=/dev/urandom,id=rng0 -device virtio-rng-pci,rng=rng0 -drive id=disk0,file=/home/free/yocto/riscv-yocto/build/tmp-glibc/deploy/images/qemuriscv64/core-image-full-cmdline-qemuriscv64-20220612021452.rootfs.ext4,if=none,format=raw -device virtio-blk-device,drive=disk0 -device virtio-tablet-pci -device virtio-keyboard-pci  -machine virt  -smp 4 -m 256 -serial mon:vc -serial null -display sdl,show-cursor=on -device bochs-display -bios /home/free/yocto/riscv-yocto/build/tmp-glibc/deploy/images/qemuriscv64/fw_jump.elf -kernel /home/free/yocto/riscv-yocto/build/tmp-glibc/deploy/images/qemuriscv64/Image--5.15.38+git0+37891dc371_cc9695f5fd-r0-qemuriscv64-20220612021452.bin -append 'root=/dev/vda rw  mem=256M ip=192.168.7.2::192.168.7.1:255.255.255.0::eth0:off:8.8.8.8 earlycon=sbi '

```
Or
```
 sudo ./tmp-glibc/work/x86_64-linux/qemu-helper-native/1.0-r1/recipe-sysroot-native/usr/bin/qemu-system-riscv64   -M virt -m 256M  -nographic -kernel  tmp-glibc/deploy/images/qemuriscv64/Image--5.15.38+git0+37891dc371_cc9695f5fd-r0-qemuriscv64-20220612021452.bin  -drive id=disk0,file=tmp-glibc/deploy/images/qemuriscv64/core-image-minimal-qemuriscv64-20220612043611.rootfs.ext4,if=none,format=raw   -device virtio-blk-device,drive=disk0 -device virtio-tablet-pci -device virtio-keyboard-pci  -append "root=/dev/vda rw console=ttyS0"
  
OpenEmbedded nodistro.0 qemuriscv64 /dev/ttyS0

qemuriscv64 login: root
root@qemuriscv64:~# lmcl
-sh: lmcl: not found
root@qemuriscv64:~# uname -a
Linux qemuriscv64 5.15.38-yocto-standard #1 SMP PREEMPT Mon May 9 20:28:10 UTC 2022 riscv64 GNU/Linux
root@qemuriscv64:~# l[   20.567072] random: fast init done
root@qemuriscv64:~# ls /dev/
autofs         initctl        ram0           ram4           stdin          tty15          tty24          tty33          tty42          tty51          tty60          ttyS3          vsock
block          kmsg           ram1           ram5           stdout         tty16          tty25          tty34          tty43          tty52          tty61          urandom        zero
btrfs-control  log            ram10          ram6           tty            tty17          tty26          tty35          tty44          tty53          tty62          vcs
char           mapper         ram11          ram7           tty0           tty18          tty27          tty36          tty45          tty54          tty63          vcs1
console        mem            ram12          ram8           tty1           tty19          tty28          tty37          tty46          tty55          tty7           vcsa
core           mtab           ram13          ram9           tty10          tty2           tty29          tty38          tty47          tty56          tty8           vcsa1
disk           null           ram14          random         tty11          tty20          tty3           tty39          tty48          tty57          tty9           vcsu
fd             port           ram15          rfkill         tty12          tty21          tty30          tty4           tty49          tty58          ttyS0          vcsu1
full           ptmx           ram2           shm            tty13          tty22          tty31          tty40          tty5           tty59          ttyS1          vda
hwrng          pts            ram3           stderr         tty14          tty23          tty32          tty41          tty50          tty6           ttyS2          vga_arbiter

```

# Programming
Todo
