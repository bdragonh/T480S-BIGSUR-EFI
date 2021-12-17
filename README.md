## 简介

- Lenovo ThinkPad T480s Hackintosh EFI ，基于OC包含基础驱动，修改三码后开箱即用。
- 适用版本：macOS Bigsur  
- 带OC引导界面主题   支持WIN10 BIGSUR双系统
- SIP正常 开启状态

## 前提

1. 更换硬盘为 Samsung SSD 970 EVO 1TB：
2. 更换网卡为 Fenvi BCM94352Z
3. 更换显示器 2.5K杜比屏 分辨率2560*1440 色彩位数8BIT(原装屏幕只是1080p 6bit会有严重的色带问题)

## 硬件说明

### 硬件配置

Lenovo ThinkPad T480s

- Intel i5-8250U
- 24GB RAM ( 8+16 )
- Samsung SSD 970 EVO 1TB
- Fenvi BCM94352Z
- 2K 8BIT屏

### 硬件使用状态

* [x] 集成显卡 UHD620 3G显存
* [x] 有线网
* [x] 无线网（隔空投屏，隔空投递）
* [x] 蓝牙 
* [x] 电池状态 
* [x] hidpi (1440*810 完美）
* [x] 声音
* [x] SD 卡读取
* [x] 触控板（多点触摸手势全开）
* [x] Fn+F1-F12 PtrSc（FN快捷键完美,PtrSc支持需要设置键盘快捷键 默认为CTRL+COMMAND+3 改为 F13）
* [x] 小红点
* [x] 雷电3 （没有测试，应该好使。）
* [x] 休眠/唤醒/关机/重启 （电源LED、合盖/开盖全部状态正常）
* [x] 个人文件保险箱 （打开后 假如看不到启动项可以按F3）
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

## 致谢

- MSzturc/ThinkpadAssistant https://github.com/MSzturc/ThinkpadAssistant
- daliansky/OC-little https://github.com/daliansky/OC-little
- kekkokk https://github.com/kekkokk/t480s_hackintosh_opencore
- GITHUB中黑苹果的所有爱好者们
