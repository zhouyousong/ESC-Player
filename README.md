# ESC-Player（base on picoreplayer）
ESC-Player是我今年业余时间对过去十来年音频和NAS工作结合后的一个小小总结\
ESC-Player is a small summary of my work on audio and NAS in my spare time this year.

![图片](https://github.com/user-attachments/assets/01148239-b4be-413e-9042-6ba21159ce8f)
![图片](https://github.com/user-attachments/assets/af7947e3-c54a-4126-b1af-e0c6931406b6)


## 原型机Prototype

ESP-Player 的原型是我在2023年底开始制作的桌面组合音箱\
The prototype of ESP-Player is a desktop combination speaker that I started making at the end of 2023.

当时我有两个老旧的设备，一个松下CD随身听，一个索尼收音机，都是陪伴我很长时间的，搬家后我希望他们能继续陪伴我，加上我也开始了对数播的研究，数播系统我花了很大的精力去选择，尝试了树莓派支持的主流系统：volumio，moode，picoreplayer，最终我觉得picoreplayer靠谱，完全开源，于是我花了半年的时间将他们集成，如下图\
At that time, I had two old devices, a Panasonic CD player and a Sony radio, both of which accompanied me for a long time. After moving, I hoped that they could continue to accompany me. In addition, I also started to study digital broadcasting. I spent a lot of energy to choose the digital broadcasting system. I tried the mainstream systems supported by Raspberry Pi: volumio, moode, picoreplayer. In the end, I felt that picoreplayer was reliable and completely open source, so I spent half a year integrating them, as shown below

![图片](https://github.com/user-attachments/assets/16e47247-b86d-45ff-ba90-8c66130be223)


这个设计有几个自己给自己挖的坑\
This design has several pitfalls that I dug for myself

1. 废旧物品怎么摆放上洞洞板是个麻烦\
1. It is troublesome to place the waste materials on the perforated board
 
----- 于是我给每个设备都手工制作了支架\
----- So I made a bracket for each device by hand
   
2. 逆向设计，如何让播放控制面板尽量简单，我希望音源切换按钮在切换音频的同时，也能切换控制接口让一套播放控制按钮能控制三个控制逻辑和电平都不一样的设备，而且还是纯硬件数字电路实现，避免日后维修找不到程序\
2. Reverse design, how to make the playback control panel as simple as possible, I hope that the audio source switch button can switch the control interface while switching the audio, so that a set of playback control buttons can control three devices with different control logic and levels, and it is also implemented by pure hardware digital circuits to avoid the program being lost in future maintenance
   
------ 于是这个板子我硬生生做了4版本,而且最后一版还带着飞线上阵，好在几乎完整实现了我的预期设想\
------ So I made 4 versions of this board, and the last version also had a flying line array, fortunately, it almost completely realized my expected idea  

3. 为了实现音频律动猫眼电子管的可视化，又引入了共地问题\
3. In order to realize the visualization of the audio rhythm cat's eye tube, the common ground problem was introduced
 
------ 幸好之前哈曼工作经历让我用了两只2元的音频变压器顺利解决\
------ Fortunately, my previous work experience at Harman allowed me to use two 2-yuan audio transformers to successfully solve the problem
   
   ![图片](https://github.com/user-attachments/assets/e71c1d0e-064f-49bd-b22c-a4b5fd377e5b)

当把这套设备最终调通后，非常开心，我对音质的追求并不高，但是每个周末的晚上可以在工作室看着音律的跳动听音乐，是非常惬意的事。\
I was very happy when I finally got this set of equipment tuned up. I don’t have high requirements for sound quality, but it is very pleasant to be able to listen to music in the studio every weekend night while listening to the rhythm of the music.

## 天使订单(Order)

在给几个老友展示了这个不算漂亮的组合后，他们给我下了两套天使订单，让我在保留这三个组合功能的情况下帮他们做漂亮点。\
After showing this not-so-pretty combination to a few old friends, they placed two angel orders with me, asking me to help them make it prettier while retaining the three combination functions.

最初我只想保留纯粹的音乐功能，但是做到一半的时候，我打算加入NAS功能，因为音乐也需要空间来存储，于是我增加了3.5寸硬盘，这个需求带来了12V供电的需求\
Initially, I only wanted to retain the pure music function, but halfway through, I planned to add NAS function, because music also needs space to store, so I added a 3.5-inch hard drive, which brought the need for 12V power supply

下图是整个ESC-Player的主要BOM\
The following figure is the main BOM of the entire ESC-Player

硬件设计很简单，框图如下，只有两块PCB是定制化设计，其他都是标准品，淘宝可买到\
The hardware design is very simple, the block diagram is as follows, only two PCBs are customized, and the others are standard products, which can be purchased on Taobao

![图片](https://github.com/user-attachments/assets/419fbf44-5d53-445a-84eb-3d71f854eea2)

**背板**：为了给3.5寸硬盘供电，在电源部分我选择了Type C输入，然后用诱骗芯片CH224K诱骗出12V，电容滤波后直接给硬盘和次级5V DCDC供电，所以供电只需要很常见的能12V输出的Tpyp C适配器即可\
**Backplane**: In order to power the 3.5-inch hard drive, I chose Type C input in the power supply part, and then used the decoy chip CH224K to decoy 12V, and directly powered the hard drive and the secondary 5V DCDC after capacitor filtering, so the power supply only requires a very common Type C adapter with 12V output

![图片](https://github.com/user-attachments/assets/4f5469ae-cab2-4d05-a80e-1c5eaa874ea1)
**按键板**：承载5个键盘按键和两个编码器旋钮\
**Keyboard**: Carries 5 keyboard keys and two encoder knobs

![图片](https://github.com/user-attachments/assets/619afebf-1cd2-4c34-b6ec-a3985d0a4673)

背板和按键板之间是IO直连的，总计5 key+2x2 Encoder = 9 IO\
The back panel and the key panel are directly connected to each other, with a total of 5 keys + 2x2 encoders = 9 IOs.
结构设计也不复杂\
The structural design is not complicated either.
胡桃木板作为底座基板，下面背挂3.5寸硬盘，上面承接亚克力支架\
The walnut board is used as the base substrate, with a 3.5-inch hard drive mounted on the bottom and an acrylic bracket on the top.
![图片](https://github.com/user-attachments/assets/887ec264-477b-4f54-a75e-8023f442554c)
![图片](https://github.com/user-attachments/assets/a9201f70-c16a-4d9b-a21b-c320d3aef142)

亚克力板做支架，承接树莓派和屏幕\
Acrylic board is used as a bracket to support the Raspberry Pi and the screen
![图片](https://github.com/user-attachments/assets/a2b20a2c-710e-4c06-9daa-7cb759d2a8f7)

这两部分的设计图纸都可以在开源资料里找到，从BOM成分上看，DIY的部分成本大概在400不到，其他的标准品占成本大头\
The design drawings of these two parts can be found in open source materials. From the BOM composition, the cost of the DIY part is less than 400, and the other standard products account for the majority of the cost.

## 功能介绍(Function introduction)

接下来介绍一下ESC-Player的功能，下面的MindMap\
Next, let me introduce the functions of ESC-Player. The following MindMap

![图片](https://github.com/user-attachments/assets/7730ef39-3451-48c7-8a32-1daf2f16824a)

主要两大功能，音乐播放器和家用NAS，围绕两大功能分别介绍一下的特点，改良的我也重点介绍一下\
The two main functions are music player and home NAS. I will introduce the features of the two functions respectively, and I will also focus on the improvements.
**音乐播放器(Music Player)**

大部分常用音源都调通了：网络收音机（需要自己添加频道，很容易），本地音乐，CD碟，Airplay（ Picoreplay 自带shairport能用作airplay串流只支持有线输出，为了能让其输出的蓝牙音箱也能被airplay串流，加入了自定义修改）\
Most common audio sources are tuned in: Internet radio (you need to add channels yourself, which is very easy), local music, CDs, Airplay (Picoreplay comes with shairport that can be used for airplay streaming and only supports wired output. In order to allow the Bluetooth speakers that it outputs to be streamed by airplay, custom modifications have been added)

Picoreplayer自带的律动频谱和UV表非常多，大家可以有很大的选择空间\
Picoreplayer comes with a lot of rhythm spectrums and UV tables, so you can have a lot of room for choice
![图片](https://github.com/user-attachments/assets/dffd5ed8-f579-4c8e-985b-cd7c5801a5b3)


**NAS**：
NAS基本上都是在原本只做文件服务共享的基础上加上了影音服务，同时把我专辑NAS里使用率最高的功能也移植了过来\
NAS basically adds audio and video services on top of the original file sharing services. At the same time, the most used functions in my album NAS are also ported over.
![图片](https://github.com/user-attachments/assets/68107e28-f943-48d2-85d7-acf70b1425fa)


1. Filebrowser，可以用网页浏览器管理文件，免去临时使用时不需要映射网络硬盘\
1. Filebrowser, you can use the web browser to manage files, eliminating the need to map the network hard disk for temporary use
   
2. Alist + Rclone + 自定义Python（开源）：网盘内容后台下载，只需要在手机网盘客户端（如百度网盘）上将想下载的文件放到指定文件夹，即可触发自动拉取到本地硬盘，实现后台下载（功率10W）\
2. Alist + Rclone + custom Python (open source): Download the network disk content in the background. You only need to put the files you want to download into the specified folder on the mobile network disk client (such as Baidu Netdisk) to trigger automatic pulling to the local hard disk and realize background download (power 10W)
   
3. 编译适配ifuse+simple-mtpfs加上自定义的python（开源）实现iphone/DJI osmo/Gopro相册一键下载到NAS指定文件夹（可增量下载）\
3. Compile and adapt ifuse+simple-mtpfs plus custom python (open source) to achieve one-click download of iPhone/DJI osmo/Gopro albums to the specified folder of NAS (incremental download is possible)
![图片](https://github.com/user-attachments/assets/680c4fee-c9e5-4261-9066-066c03463779)

4. Jellyfin适配，网页或者手机客户端可实现看片自由、
4. Jellyfin is compatible, you can watch movies freely on the web or mobile client
![图片](https://github.com/user-attachments/assets/628795ef-3d84-4919-8772-33326495b787)

5. Navidrome适配，可在手机上自由自在听NAS里的本地音乐、
5. Navidrome compatible, you can listen to local music in NAS on your mobile phone freely
![图片](https://github.com/user-attachments/assets/d064c949-a416-40b4-9023-757f5092d8af)

当时为了远程SSH support我的朋友做一些问题修复，我部署了frpc，可以在网页上一键打开或关闭远程访问，这必然也是一个安全隐患，欢迎大家审查代码，我只是FRPC的使用者\
At that time, in order to remotely SSH support my friends to fix some problems, I deployed frpc, which can open or close remote access with one click on the web page. This is definitely a security risk. Welcome to review the code. I am just a user of FRPC.

**其他开发中的功能(Other features in development)**

公网访问：适配DDNS动态域名IP更新，带公网IP的家庭网络配合域名（一年30左右）可实现广域网访问，可在任何地点访问个人NAS服务\
Public network access: Adapt to DDNS dynamic domain name IP update, home network with public network IP and domain name (about 30 per year) can achieve wide area network access, and personal NAS service can be accessed from any location

NFC选歌：通过NFC刷卡的方式调出专辑，让选专辑实现实体化\
NFC song selection: call up albums by swiping NFC cards, making album selection a physical reality
#
**以上就是ESC-Player的主要功能，所有的源码都是python+shell编写，未编译未加密运行，镜像放在百度网盘**\
**The above are the main functions of ESC-Player. All source codes are written in python+shell, run without compilation and encryption, and the image is placed on Baidu network disk.**

![图片](https://github.com/user-attachments/assets/09451c24-91bc-473c-8639-d3affb0ce967)

欢迎大家Copy使用，我也会持续开发一些实用的功能，让他释放出更多的能力\
Welcome to copy and use, I will continue to develop some practical functions to release more capabilities

欢迎关注我B站账号ZhouYousong，后续有陆续出视频说明。如遇到问题的可以加我wx：zhou-yousong。也欢迎有兴趣量产的朋友联系合作\
Welcome to follow my B station account ZhouYousong, and I will release video instructions later. If you encounter any problems, you can add me on WeChat: zhou-yousong. Friends who are interested in mass production are also welcome to contact us for cooperation
