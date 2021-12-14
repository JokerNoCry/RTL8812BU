# RTL8812BU

# Kali 5.14内核安装 RTL 8812BU 网卡驱动

> shell命令最好一行一行输入，避免中间有些步骤执行失败，任何一步失败都有可能导致驱动安装失败。

> 88x2bu-5.8.7.4.zip 为88x2bu系列网卡的驱动程序源代码，来源于github。

## 更新并安装依赖包

```sh
sudo su
apt update
apt upgrade
reboot

apt install unzip
apt install libelf-dev
apt install make-guile
apt install gcc dkms bc
apt install libncurses5-dev libncursesw5-dev
```

## 下载驱动代码并复制到Kali中并解压
```sh
sudo su
cd ~
git clone https://github.com/JokerNoCry/RTL8812BU
cd RTL8812BU
unzip 88x2bu-5.8.7.4.zip
cd 88x2bu-5.8.7.4 
make
make install
reboot
```

重启之后插上网卡，使用``ifconfig``或``iwconfig``等的命令查看是否有wlan0即可。

## Monitor模式和Managed模式的切换

### 查看网卡名称
```sh
iwconfig
```
假设网卡名为wlan0

### RTL8812BU 切换为 监听模式(Monitor)
```sh
ip link set wlan0 down
iwconfig wlan0 mode monitor
ip link set wlan0 up
```

### RTL8812BU 切换为 托管模式(Managed)
```sh
ip link set wlan0 down
iwconfig wlan0 mode managed
ip link set wlan0 up
```
