
WEB:

https://wiki.realtek.com/display/PON/openwrt-24.10

Created by Seven Lee on 2025/08/27
##Download OpenWRT 24.10
repo init -u ssh://cn2sd5.rtkbf.com:29418/rlxlinux/manifest -m rtkwrt.xml

repo sync -d; repo start my-topic --all

##Setup preconfig
For 9607F
./setup_openwrt.sh 9607F_demo_Board
Preliminary work
singularity shell /home/share/singularity/openwrt.simg
cd openwrt-24.10
##Compiling
make menuconfig
make kernel_menuconfig
make or make V=s (加上V=s 會顯示編譯過程，時間會拉長)
##Image location
openwrt-24.10/images
##Initial script

/etc/init.d/diagshell

##/etc/scripts/modutils.sh (get PON_MODE and PON_SPEED to /proc/ca_rtk/ponmisc) → /etc/insdrv.sh → /etc/runsdk.sh → /etc/runomci.sh

##/etc/init.d/diagshell file location
../package/realtek/diagshell/files/diagshell.init
##/etc/scripts/modutils.sh file location
../package/realtek/diagshell/files/modutils.sh
#Only compiler diagshell

make package/realtek/diagshell/clean

make package/realtek/diagshell/compile V=s

make package/install; make target/install (generate image)

#Only compiler ca_packages

make ppackage/kernel/realtek/ca_packages/clean

make package/kernel/realtek/ca_packages/compile V=s

make package/install; make target/install

#Only compiler linux

make target/linux/clean

make target/linux/compile V=s

make package/install; make target/install

MIB file location

../package/realtek/rtk_base/files/rtkmib

../package/realtek/rtk_mib/src/
../package/realtek/rtk_configd/
OMCI file location
../v24.10/target/files-6.6/drivers/net/ethernet/realtek/rtl86900/sdk/src/app/omci_v1/OMCI/src/omci_mib.c
Build folder location
./build_dir/target-aarch64-openwrt-linux-gnu_glibc/linux-realtek_bb_rtl9607f/ca_packages
./build_dir/target-aarch64-openwrt-linux-gnu_glibc/linux-realtek_bb_rtl9607f/linux-6.6.93/drivers/net/ethernet/realtek/rtl86900/
