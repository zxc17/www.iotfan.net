## Linux环境下Wireshark抓包总结

Windows下捕获不到IEEE802.11数据。

### 1. Wireshark安装与配置
1. 安装软件

```bash
sudo apt-get install wireshark
sudo apt-get install wireshark-gtk
```
2. 查询系统有无无线网卡，捕获802.11数据帧时需要开启无线网卡，输入：``iwconfig``
```bash
lo       no wireless extensions.
wlx64fb816ae233  IEEE 802.11  ESSID:off/any  
          Mode:Managed  Access Point: Not-Associated   Tx-Power=0 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          
ens33     no wireless extensions.
```
wlx64fb816ae233就是无线网卡的名字，后面列出了无线网卡的一些状态信息。
```bash
sudo iw dev wlx64fb816ae233  interface add mon0 type monitor
sudo ifconfig mon0 up
sudo wireshark-gtk
```
Wireshark运行时需要root权限，并会弹出警告，忽略即可。然后就会进入Wireshark的程序界面，选择我们新添加的mon0接口，点击`start`，程序自动开始捕获数据。

### 2. Wireshark Filter（过滤器）
Wireshark捕获数据时可能会存在大量我们不需要的数据帧，因此过滤
Capture Filter和Display Filter。
顾名思义，Capture Filter是在捕获阶段进行过滤的，不符合条件的数据会被Wireshark直接丢弃，可以避免这些数据占用太多内存或存储空间。
而Display Filter是在显示时发挥作用，不符合过滤条件的数据依然会被捕获，只是不显示而已。
需要注意的是Capture Filter和Display Filter两者