# Hackintosh ASUS TUF-B460M-PRO
```
基于opencore 0.9.1
由https://github.com/VanXNF/Hackintosh-Gigabyte-B460M-Aorus-Pro 修改而来，特此感谢
```

&ensp;

## 硬件平台
| 设备 | 型号 | 说明 |
|:---:|:---| :--- |
| CPU | 10500 es | QRSK |
| 主板 | asus b460m pro | cfg lock默认开启了，无此选项 |
| 内存 | 金百达 长鑫a-die 3600 | 从AMD平台拆下来的,兼容性不错 |
| 集成显卡 | Intel UHD Graphics 630 | |
| 独立显卡 | amd rx5500xt 4G | 免驱 |
| 无线网卡 & 蓝牙 | fenvi t919 | 免驱 |

&ensp;
## 修改点
### DeviceProperties 部分
* PciRoot(0x0)/Pci(0x1,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)
我这边无显卡电感啸叫问题，这里我删除了
* PciRoot(0x0)/Pci(0x2,0x0)
这里 我是独立显卡， 选择 0300C89B， 如果仅独显要自己修改
* PciRoot(0x0)/Pci(0x1F,0x3)
* PciRoot(0x0)/Pci(0x1F,0x6)
声卡和有线网卡， 对照主板参数修改

&ensp;

### Kernel 部分
```
用户如在 BIOS 中禁用了 VT-D 选项，可在此处将值设置为false。
我这里是biso中关闭了vt-d
```

&ensp;

### Misc 部分
```
经过多次迭代，本 EFI 已较为稳定，因此取消了 DEBUG 调试信息输出，初次安装或有调试需要可以在 Debug 部分，开启 AppleDebug、ApplePanic 选项，并指定日志输出 Target 值为 67。
这里我也是直接用了，没有修改
```

&ensp;
### NVRAM 部分
还是直接贴别人的修改, 需要注意的是没有独显，启动参数要修改
```
使用 4K 以下分辨率屏幕的用户可以将 4D1EDE05-38C7-4A6A-9CC6-4BCCA8B38C14 中的 UIScale 值调整为 01。

未使用 RX5000/RX6000 系列显卡的用户需要将 7C436110-AB2A-4BBB-A880-FE41995C9F82 中的 boot-args 中的 agdpmod=pikera 参数移除。

需要启用 DEBUG 的用户需要在 7C436110-AB2A-4BBB-A880-FE41995C9F82 中的 boot-args 中添加参数 -v debug=0x100 keepsyms=1。
```

&ensp;
### PlatformInfo 部分
```
本 EFI 将机型设定为 iMac20,1，有需要请自行更改。
SystemSerialNumber、SystemUUID 和 MLB。已经移除， 需要自己生成添加
可使用GenSMBIOS工具生成
```

&ensp;

## 电源相关设置
在终端依次执行以下指令或使用 HackinTool 修复电源选项，可有效防止睡眠引发系统崩溃。
```
sudo pmset autopoweroff 0
sudo pmset powernap 0
sudo pmset standby 0
sudo pmset proximitywake 0
sudo pmset tcpkeepalive 0
```
![imnage](https://github.com/stroll-z/Hackintosh-ASUS-TUF-B460M-PRO/blob/main/2023-05-11%2000.00.27.jpg)

