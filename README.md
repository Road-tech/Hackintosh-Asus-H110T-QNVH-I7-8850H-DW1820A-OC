# Hackintosh for Asus-H110T, QNVH(8850hes), DW1820A, using Opencore and Support macOS Big Sur  

![image](https://github.com/Road00/Hackintosh-AsusH110T-QN8J-I7-8700Tes--DW1820A-Opencore/blob/master/figure/0000.jpg?raw=true)  

---

**使用EFI前请务必修改三码(SSN,UUID,ROM)**    
**Please change three system codes (SSN,UUID,ROM) before using this EFI**   

---

# Hardware/硬件
|  | Specifications / 型号 | Note / 备注 |
|-------------------------|:---------------------------------:|:-------------------------------:|
| Motherboard/主板: | Asus H110T | Thin ITX |
| CPU/处理器: | QNVH | I7 8850h ES |
| CPU Cooler/散热器: | Nimitz Diy Mac Mini 3D-printing cooling kit | [Nimitz 超盒 3D打印散热套件](https://m.tb.cn/h.VSRHxNg?sm=8e19ac) |
| Hard Drive/硬盘: | Customization SSD using SM2263XT and 512g Intel TLC NAND Flash | [NVME 固态套料 主控板2263XT](https://m.tb.cn/h.VSA0n4u?sm=086db2) |
| RAM/内存: | SEIWHALE 16G DDR4 2666MHz X2 | [枭鲸 16G DDR4 2666 笔记本电脑内存条](https://item.taobao.com/item.htm?id=612747898988) |
| Wireless Card/无线网卡: | BCM94350ZAE | DW1820A |
| Tower Case/机箱: | Mac mini teardown case拆机机箱 | Mac mini 拆机机箱 |
| Power/电源: | Dell 74/50mm 19v 130w DC power adapter |  |
  
---
# Functions/功能
### Work：
- HDMI port (1080p) ｜ HDMI接口
- DP port (1080p) ｜ DP接口
- Audio output on HDMI ｜ HDMI接口音频输出
- All USB ports ｜ 所有USB接口
- Wi-Fi & Bluetooth ｜ Wi-Fi & 蓝牙
- Dual Network Interface Card ｜ 双千兆
- 3.5mm Audio Output & Mic Input ｜ 3.5mm音频输出
- Airdrop ｜ 隔空投送
- AirPlay ｜ 投屏
- Continuity ｜ 接力   
- hyper-threading ｜ 超线程

### Not tested yet:
- Sleep ｜ 睡眠
- 4k display ｜ 4K输出  （我没有4K屏）
  
---

# Backup MAC address/备份MAC地址:

Asus H110T has two network interface cards(NIC):  

* Realtek® RTL8111H  
* Intel® I219V  

Asus write the Intel NIC's MAC address into BIOS. To using 8th generation CPU on H110T, we need to flash the modify BIOS into motherboard. But the MAC address will lost after flash the modify BIOS and the MAC address will become ```88:88:87:88```. So backup the NIC MAC address firstly. 

You has two ways to find the MAC address:   

* Check the motherboard, MAC address usually on the memory slots.   
* Using command ```ipconfig``` on Windows or ```ifconfig``` on macOS\Ubuntu to get MAC address   

华硕H110T这块主板有两张网卡：

* Realtek® RTL8111H  
* Intel® I219V  

华硕把Intel网卡的MAC地址写在了BIOS里面，但是在为了支持8代CPU去魔改BIOS之后，会丢失Intel网卡的MAC地址。 具体表现为Intel网卡的MAC地址会变成```88:88:87:88```，所以要先备份MAC地址。

有两个方法去查MAC地址：

* 主板的内存槽上贴着MAC地址，Intel网卡通常是左边那个
* Windows下用 ```ipconfig``` 或者 macOS/Linux下用 ```ifconfig```去查MAC地址

![image](https://github.com/Road00/Hackintosh-AsusH110T-QN8J-I7-8700Tes--DW1820A-Opencore/blob/master/figure/100.jpg?raw=true)  


---

# Flash modify BIOS/刷入魔改BIOS

You need to prepare a device programmer like ch341a, GZU OnePro(Recommend),

BIOS在上图左下角红框的位置，拔下来刷入。
**建议使用编程器刷入BIOS！**

当然你也可以尝试软刷bios，具体教程和BIOS文件都打包在[H110T-ASUS-4212.zip](https://github.com/Road-tech/Hackintosh-AsusH110T-QNVH-I7-8850H-DW1820A-OC/raw/main/H110T-ASUS-4212.zip)

---

# Recover MAC address/恢复MAC地址

请准备以下工具：

* 任意容量的U盘      
* Rufus  		[下载地址](https://rufus.ie/zh_CN.html)     
* EEUPDATE 	[下载地址](https://github.com/Road-tech/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-Opencore/raw/master/Eeupdate.rar)    

恢复MAC地址流程：

1. 打开Rufus，格式化U盘，制作DOS启动盘。
2. 解压并复制EEUPDATA文件到U盘（假设EEUPDATA放在MAC文件夹内）。
3. U盘插入机子，进入BIOS设定U盘启动，进入DOS系统。
4. 输入 ```dir``` 查看文件。
5. 输入  ```cd MAC``` 进去MAC文件夹。
6. 输入  ```eeupdate /nic=1 /mac=XXXXXXXXX``` 恢复MAC地址，```XXXXXXXXX```为你的记录的MAC地址。
7. 提示成功后重启，进任意操作系统查看网卡MAC地址是否恢复成功。

---

# BIOS setting/BIOS设定：

### Disable：
- Fast Boot  
- CFG Lock   
- VT-d  
- CSM  
- Intel SGX  

### Enable：
- Intel Virtualization Technology   
- Above 4G decoding  
- Hyper Threading 
- Serial Port 
  
---
  
# Install macOS/安装macos

请准备以下工具：
* 系统镜像：请自备 macOS Big Sur 11.2.3 安装镜像   
* OC编辑工具：OpenCore Configurator [下载地址](https://mackie100projects.altervista.org/)    
* 镜像写入工具：Etcher （Windows，macOS，Linux皆可运行） [下载地址](https://www.balena.io/etcher/)    
* 我提供的OC引导的EFI：[下载地址](https://github.com/Road-tech/Hackintosh-AsusH110T-QNVH-I7-8850H-DW1820A-OC.git)    
* 准备一个大于10g的u盘    

安装过程我就不重复了，大家可以参考下[我之前的文章](https://post.smzdm.com/p/adwrg48d/)。

安装完成后请记得模拟NVRAM：
请在安装完系统后将增加 **LogoutHook** 文件用于放置在任意位置。并且在终端输入：
 ```sudo defaults write com.apple.loginwindow LogoutHook /path/to/LogoutHook.command```

比如你放在**下载**文件夹内： 
```sudo defaults write com.apple.loginwindow LogoutHook /Users/xjn/Documents/LogoutHook/LogoutHook.command```

重启后，你会在/EFI/下看到nvram.plist，代表已经成功模拟了。

**！运行后不要删除补丁包 ！**

---

# More Detail/安装细节

![image](https://github.com/Road00/Hackintosh-AsusH110T-QN8J-I7-8700Tes--DW1820A-Opencore/blob/master/figure/001.jpg?raw=true)  
全家福
![image](https://github.com/Road00/Hackintosh-AsusH110T-QN8J-I7-8700Tes--DW1820A-Opencore/blob/master/figure/002.jpg?raw=true)  
QN8J，35w，6核12线程，1.6GHz默频
![image](https://github.com/Road00/Hackintosh-AsusH110T-QN8J-I7-8700Tes--DW1820A-Opencore/blob/master/figure/003.jpg?raw=true)  
屏蔽+短接
![image](https://github.com/Road00/Hackintosh-AsusH110T-QN8J-I7-8700Tes--DW1820A-Opencore/blob/master/figure/004.jpg?raw=true)  
硬件合体，不知道枭鲸知不知道他家的内存贴纸贴反了
![image](https://github.com/Road00/Hackintosh-AsusH110T-QN8J-I7-8700Tes--DW1820A-Opencore/blob/master/figure/005.jpg?raw=true)  
请出尼米兹散热器
![image](https://github.com/Road00/Hackintosh-AsusH110T-QN8J-I7-8700Tes--DW1820A-Opencore/blob/master/figure/006.jpg?raw=true)  
将弹簧放在风道主体，然后把纯铜散热器压上去
![image](https://github.com/Road00/Hackintosh-AsusH110T-QN8J-I7-8700Tes--DW1820A-Opencore/blob/master/figure/007.jpg?raw=true)  
把散热背板放在主板后面，然后把风道主体压上去，最后上螺丝拧紧。
这一步超级反人类！假象一下，弹簧并不能固定在主体上，散热器也不能，你要把它倒扣在主板上还要保证主体-弹簧-散热之间不能移位。最后你还要确保主体的螺丝孔能够对得上散热器的背板。
![image](https://github.com/Road00/Hackintosh-AsusH110T-QN8J-I7-8700Tes--DW1820A-Opencore/blob/master/figure/008.jpg?raw=true)  
这个安装反人类到我不想装第二次！ 所以请尽量保证机子可以正常开机后再进行装机。
**请务必注意四颗螺丝的受力尽量均匀且不会过紧，不然可能会压弯主板！**
![image](https://github.com/Road00/Hackintosh-AsusH110T-QN8J-I7-8700Tes--DW1820A-Opencore/blob/master/figure/009.jpg?raw=true)  
装上后IO板之后就可以推进机箱了！同时别忘了接上Wi-Fi天线。
![image](https://github.com/Road00/Hackintosh-AsusH110T-QN8J-I7-8700Tes--DW1820A-Opencore/blob/master/figure/010.jpg?raw=true)  
成功合体！推入过程不会太顺畅的，要按压一下，刚刚能推进去。
![image](https://github.com/Road00/Hackintosh-AsusH110T-QN8J-I7-8700Tes--DW1820A-Opencore/blob/master/figure/011.jpg?raw=true)  
最后装上风扇，这里可以看到3d打印的纹路，很粗糙
![image](https://github.com/Road00/Hackintosh-AsusH110T-QN8J-I7-8700Tes--DW1820A-Opencore/blob/master/figure/012.jpg?raw=true) 
![image](https://github.com/Road00/Hackintosh-AsusH110T-QN8J-I7-8700Tes--DW1820A-Opencore/blob/master/figure/013.jpg?raw=true) 
接下来就是重量嘉宾，大佬设计打印的网孔底盖！
![image](https://github.com/Road00/Hackintosh-AsusH110T-QN8J-I7-8700Tes--DW1820A-Opencore/blob/master/figure/014.jpg?raw=true) 
还是很精致漂亮的
![image](https://github.com/Road00/Hackintosh-AsusH110T-QN8J-I7-8700Tes--DW1820A-Opencore/blob/master/figure/015.jpg?raw=true) 
完美装上，严丝合缝
![image](https://github.com/Road00/Hackintosh-AsusH110T-QN8J-I7-8700Tes--DW1820A-Opencore/blob/master/figure/016.jpg?raw=true) 
换个角度
![image](https://github.com/Road00/Hackintosh-AsusH110T-QN8J-I7-8700Tes--DW1820A-Opencore/blob/master/figure/017.jpg?raw=true) 
装上小辣椒天线
![image](https://github.com/Road00/Hackintosh-AsusH110T-QN8J-I7-8700Tes--DW1820A-Opencore/blob/master/figure/018.jpg?raw=true) 
![image](https://github.com/Road00/Hackintosh-AsusH110T-QN8J-I7-8700Tes--DW1820A-Opencore/blob/master/figure/019.jpg?raw=true) 

---

# Performance/系统展示

![image](https://github.com/Road00/Hackintosh-AsusH110T-QN8J-I7-8700Tes--DW1820A-Opencore/blob/master/figure/102.PNG?raw=true) 

---
# Reference/参考

[精解OpenCore](https://blog.daliansky.net/OpenCore-BootLoader.html) - [黑果小兵的部落阁 ](https://blog.daliansky.net/)

[使用OpenCore引导黑苹果](https://blog.xjn819.com/?p=543) - [XJN](https://blog.xjn819.com/) 

[Asrock deskmini 310-com hackintosh 10.14-10.15 EFI](https://blog.xjn819.com/?p=7) - [XJN](https://blog.xjn819.com/)

[DW1820A/BCM94350ZAE/BCM94356ZEPA50DX插入的正确姿势](https://blog.daliansky.net/DW1820A_BCM94350ZAE-driver-inserts-the-correct-posture.html) - [黑果小兵的部落阁](https://blog.daliansky.net/)

[华硕 ASUS H110T 支持 8 代 9 代 Xeon BIOS](http://www.smxdiy.com/thread-1862-1-1.html) - [D大](http://www.smxdiy.com/space-uid-1196.html)
