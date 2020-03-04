# Hackintosh-ASUS-FXPRO-GL552VW
    This is for Asus Flying Fortress FX-PRO 2016（I7-6700HQ HD530）
    This guide maybe help you run Catalina (Beta 10.15) Mojave（10.14.0-10.14.6） & High Sierra（10.13.6） on your laptop
    And I will list all the problem while the installation
<br> 

![](https://timgsa.baidu.com/timgimage&quality=80&size=b9999_10000&sec=1568630772264&di=6d4d76d259007c763e302354403cbc64&imgtype=0&src=http%3A%2F%2Fimage3.buy.ccb.com%2Fimages%2F68397788%2F1455696762755_4.jpg)  

First I will list my configuration of my laptop
写的比较乱，我就不排版了 比较忙
<br>
2020-3-4日
更新内容lilu-1.4.1
AppleAlc-1.4.6
Cloverbootloader-5103
macos Catalina10.15.3正式版（理论上之前所有版本的系统均可安装）
新增功能内容：增加HDMI输出，但有缺陷，必须开机后插入hdmi,如果开机带外接显示器开机内屏会只有背光，有能力的可以自行解决，联系我更改
<br> 

|HARDWARE | DETAIL |
|--|--|
| CPU | INTEL I7-6700HQ |
| IGPU | HD530 |
| EGPU | GTX960M (Shield By WEG.KEXT) |
| IGPU | HD530 |
| MEMORY | SK HYNIX 4G*2 2133MHz|
| Display | AUO TN 1080P |
| SSD | WD GREEN SATA 240G （NVME is not supported） |
| TouchPad | ELAN 1000 |
| Sound | Conexant 20751/2 |
| wifi | Broadcom 94350（1820A）or AR9565（Blooteeth not avilible） |

<br> 

* Other environment
    * Dual-booting Windows 10&Ubuntu on my Laptop

<br> 

# How to install？

<br>
    1.You must have a 8G USB，
    2.Download my EFI and replace your efi folder
    3.After several reboot the installation will complete
<br>

## Graphics IGPU
Integrated Intel HD530 support is handled by WhateverGreen, and configured in the PciRoot(0x0)/Pci(0x2,0x0) section of config.plist. The Nvidia GPU is not supported due to hardware differences and lack of driver support in macOS. It is disabled to save power.  Besides, when I fix the panic of sleep,I find EGPU will disturb the process， bootargs of WEG -wegnoegpu is so good，you will not like ssdt-DGPU.aml.its so easy,is not that?

<br>

# The backlight control is work 
You only need put ssdt-PNLF.aml and WhateverGreen.kext

# Keyboard & TouchPad
My keyboard is ps/2 type
only need VoodooPS2controller.kext

<br>
Touchpad :Elan 1000
finger gesture fully supported
VoodooI2C.kext &VoodooElan.kext
work in interrupt mode very well，thanks for developer of VoodooI2C

<br>

Alexandred(https://voodooi2c.github.io/）

<br>
If your BIOS VERSION is 304,you can use my dsdt.aml to make your touchpad work
sorry now I did not used hotpatch for touchpad ，because nowdays i need to attend to my class,lessly spare time.
Sonner or later i will improve it!

<br>

I think the 304 bios is good ,you can update ,and use my EFI to make your touchpad work,not complex.
## WIFI&BLUETOOTH
* AR9565 
  * Its a vrey good card . If you are not a Perfectionist， this card can do almost everything, you dont have to change it.
Sadly! I am!  I think airdrop is essential. So I buy a Broadcom 1820A.I will also put the driver to my EFI ,if you need this,you only need drag IO80211Familly.kext to the Kext Utility. restart, and then enjoy it.

* BCM 94350 (1820A)
  * In China ,with Hackintosh popularizing，more and more wifi card of macbook is increasing ，for example，The price of BCM 1560 almost 350 yuan（50💲），its too expensive for a university student to buy. 
  
  <br>
  But I see the 1820A guide of heiguoxiaobing,Very well received 
  <br>
  （https://blog.daliansky.net/DW1820A_BCM94350ZAE-driver-inserts-the-correct-posture.html）
  <br>
  no english,lol .
  <br>
    If you are not Chinese,you should change the bootargs for yourself!!!!!!!!!!!!!!!!!
    <br>
    
    brcmfx-country=    brcmfx-driver= 
    you can also see acidanthera 
    https://github.com/acidanthera/AirportBrcmFixup
    add pci root&detail
    
    <br>
    
# Battery Status
Thanks for VirtualSmc ,I dont need to edit my dsdt to make my battery work,Install SMCBatteryManager.kext that comes with VirtualSMC to get battery status. Ensure that you have removed ACPIBatteryManager if you’ve installed it previously.
# Audio
  By using new Layout Id 21,cx20751/2 can work in a good condition. (microphone&Speaker can work in the same time)
  <br> 
# Usb
# TouchId
Since we’re using the MacBookPro13.3 SMBIOS, macOS is expecting Touch ID to be available, causing lag on password prompts. This can be disabled for now with the NoTouchID kext.

Install NoTouchID.kext
  <br>
  
# Sleep
Using Hackintool fix sleep mode , test,sleep is work very well .Hibernation also work.
------------------------------ Not compelete---------------------------
