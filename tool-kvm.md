```
Author: holdlg
Last updated: 2016-03-07 10:23:04
```

# 安装
1.ubuntu14 安装命令

```
sudo apt-get install qemu-kvm qemu
sudo apt-get install virt-manager virt-viewer libvirt-bin
```
2.创建磁盘
```
sudo qemu-img create -f qcow2  winxp.img 10G
```
- qemu-img 是命令
- qcow2 是磁盘格式
- winxp.img 是磁盘
- 10G 磁盘大小

3.创建镜像
```
sudo qemu-system-x86_64 -hda win_xp_sp3.img -cdrom xp_sp3.iso -boot d
```
- qemu-system-x86_64 是命令
- -hda 指定第一块磁盘
- -cdrom 指定镜像位置
- -boot d  从光驱启动
- -boot c 从硬盘启动

4.图形化管理工具 **推荐**
```
   virt-manager
```

# 安装中的bug
1. 找不到SDL,提示

```
Could not initialize SDL(No available video device) - exiting
```

- 第一种方法是：桌面登录执行，不要使用命令行工具如：putty
- 第二种方法是：

    ```
    sudo apt-get remove libsdl1.2debian
    sudo apt-get install libsdl1.2-dev
    ```
    [http://www.libsdl.org/](http://www.libsdl.org/)下载 SDL 1.2,然后执行：
    ```
    解压sdl1.2包,并进入目录
    ./configure
    make
    make install
    ```

# 格式转换
1.raw转换为qcow2
```
qemu-img convert -f raw -O qcow2 xp.img xp.qcow2
```

# 桥接网络
1.修改网络eth0的配置
```
auto eth0
iface eth0 inet manual

```
2.添加网络br0的配置
```
auto br0
iface br0 inet static
address 192.168.10.45
netmask 255.255.255.0
network 192.168.10.0
broadcast 192.168.10.255
gateway 192.168.10.50
dns-nameservers 114.114.114.114
bridge_ports eth0
bridge_fd 9
bridge_hello 2
bridge_maxage 12
bridge_stp off

```
- 网络br0的配置信息是原来eth0的，否则不不能访问外网

3.ubuntu14下完整的配置
```
# interfaces(5) file used by ifup(8) and ifdown(8)
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet manual

auto br0
iface br0 inet static
address 192.168.10.45
netmask 255.255.255.0
network 192.168.10.0
broadcast 192.168.10.255
gateway 192.168.10.50
dns-nameservers 114.114.114.114
bridge_ports eth0
bridge_fd 9
bridge_hello 2
bridge_maxage 12
bridge_stp off

```
4.虚拟机网络的配置
- 使用virt-manager工具，可以在创建虚拟机时进行配置选择桥接br0网络
