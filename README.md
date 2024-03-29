## [English](https://github.com/bdragonh/T480S-BIGSUR-EFI/blob/master/en.md)

## 支持Monterey  support Monterey  支持Bigsur  support Bigsur

## 简介

- Lenovo ThinkPad T480s Hackintosh EFI ，基于OC包含基础驱动，修改三码后开箱即用。
- 适用版本：macOS Bigsur  , macOS Monterey
- 带OC引导界面主题   支持WIN10 MACOS双系统安全 （但不建议 最好使用PD虚拟机）
- SIP正常 开启状态

## 最优越体验方案

1. 更换硬盘为 Samsung SSD 970 EVO 1TB：
2. 更换网卡为 Fenvi BCM94352Z
3. 更换显示器 2.5K杜比屏 分辨率2560*1440 色彩位数8BIT(原装屏幕只是1080p 6bit会有严重的色带问题)


### EFI自测试硬件配置

Lenovo ThinkPad T480s

- Intel i5-8250U
- 24GB RAM ( 8+16 )
- Samsung SSD 970 EVO 1TB
- Fenvi BCM94352Z
- 2K 8BIT屏
 
### SMBIOS MacBookPro15,2
- 支持 Monterey下隔空投屏分共享

### 硬件使用状态

* [x] 集成显卡 UHD620 3G显存
* [x] 有线网
* [x] 无线网
* [x] 蓝牙 （隔空投递-需换网卡）
* [x] 电池状态 
* [x] hidpi (1440*810 完美）
* [x] 声音
* [x] SD 卡读取
* [x] 触控板（多点触摸手势全开）
* [x] Fn+F1-F12 PtrSc（FN快捷键完美,PtrSc支持需要设置键盘快捷键 默认为CTRL+COMMAND+3 改为 F13）
* [x] 小红点
* [x] 雷电3 （没有测试，应该好使。）
* [x] 休眠/唤醒/关机/重启 （电源LED、合盖/开盖全部状态正常）
* [x] 个人文件保险箱 
* [x] USB全部端口 （多个USB不会出现供电问题）
* [x] 风扇状态获取正常 （加入风扇控制驱动 拒绝发热）
* [ ] ~~启动转换助理~~ （建议使用parallels desktop虚拟机运行WINDOWS）
* [ ] ~~独立显卡 mx150~~ (无解并且永远无解 只能使用集成显卡)
* [ ] ~~指纹识别器~~ （无解并且永远无解 只能使用密码输入）

## 使用方法

- 复制EFI到EFI分区 编辑EFI/OC/config.plist 修改SystemSerialNumber、SystemUUID、MLB三码
- 改快捷键设置  【将屏幕图片存储成文件】 改为 PrtSc 备注：看到快捷提示为F13即可 

## 必装工具 

- one-key-hidpi : 一键开启 macOS HiDPI
- ThinkpadAssistant : 开启THINKPAD驱动FN多功能键位
- YogaSMCNC : 可以控制风扇速度 是自动或者自定义转速
- Hackintool : 打开后 选择电源选项卡 点击修复按钮 （重要，一定要操作 超长时间待机防止写入硬盘 不然无法唤醒）
 
## 不同系统版本系统指南

- Bigsur和Monterey 使用发布版本Bigsur&Monterey https://github.com/bdragonh/T480S-BIGSUR-EFI/releases/
- Catalina系统的 使用发布版本Catalina https://github.com/bdragonh/T480S-EFI/releases/tag/Catalina

## 支持Bigsur升级至Monterey OTA升级流程

- 打开换EFI分区，替换EFI版本至BIGSUR&MONTEREY版本。 注意！换后不需要重启系统！
- APP STORT中搜素 MACOS MONTEREY 下载并安装即可。

## 支持BIGSUR和MONTEREY的全新安装
- 根据教程获取一个装备好的U盘 https://support.apple.com/zh-cn/HT201372
- 使用OpenCore Configurator打开U盘EFI分区 把Bigsur&Monterey版本的EFI复制进去

## 已知问题
- BIGSUR下已经完美（当然独立显卡和指纹识别就不要期待了）
- MONTEREY下隔空投递有一个BUG 你无法投递文件到其它MACOS的PC机上但可以接受文件 发送和接受来自手机的场景是OK的（此BUG已经反馈开发者 等待修复中）
- 如果你的T480S使用的原装网卡。你无法使用[隔空投递]与[随航]
- 蓝牙重启不会自动连接 休眠唤醒偶尔失灵 下面是解决办法
```
1.休眠唤醒的时候
   brew install sleepwatcher
   brew install blueutil
   brew services start sleepwatcher
   touch .sleep
   touch .wakeup
   chmod 755 .sleep
   chmod 755 .wakeup
  之后编辑上面的内容为如下
   >cat .sleep
    networksetup -setairportpower en0 off
    /usr/local/bin/blueutil --power 0
    #第一行为断开WIFI网络 休眠了还是断网安全一些

   >cat .wakeup
    networksetup -setairportpower en0 on
    /usr/local/bin/blueutil --power 1
    sleep 2
    /usr/local/bin/blueutil --connect 70-26-05-10-f2-3c
    #第一行为断开WIFI网络 休眠了还是断网安全一些 
    #—connect下面是你蓝牙设备的MAC地址 需要提前连接过此设备 执行blueutil —recent可以查看你想连接的蓝牙MAC越来越

  2.重启或开机的时候
   使用mac自带的【自动操作】APP创建一个执行脚本的APP内容如下
   /usr/local/bin/blueutil --power 0
   sleep 2
   /usr/local/bin/blueutil --power 1
   sleep 2
   /usr/local/bin/blueutil --connect 70-26-05-10-f2-3c
   #—connect下面是你蓝牙设备的MAC地址 需要提前连接过此设备 执行blueutil —recent可以查看你想连接的蓝牙MAC越来越
```                 
## 致谢

- MSzturc/ThinkpadAssistant https://github.com/MSzturc/ThinkpadAssistant
- daliansky/OC-little https://github.com/daliansky/OC-little
- acidanthera https://github.com/acidanthera
- GITHUB中黑苹果的所有爱好者们
