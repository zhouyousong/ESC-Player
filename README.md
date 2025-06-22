# ESC-Player
ESC-Player是我今年业余时间对过去十来年音频和NAS工作结合后的一个小小总结

![图片](https://github.com/user-attachments/assets/01148239-b4be-413e-9042-6ba21159ce8f)
![图片](https://github.com/user-attachments/assets/af7947e3-c54a-4126-b1af-e0c6931406b6)


## 原型机

ESP-Player 的原型是我在2023年底开始制作的桌面组合音箱

当时我有两个老旧的设备，一个松下CD随身听，一个索尼收音机，都是陪伴我很长时间的，搬家后我希望他们能继续陪伴我，加上我也开始了对数播的研究，数播系统我花了很大的精力去选择，尝试了树莓派支持的主流系统：volumio，moode，picoreplayer，最终我觉得picoreplayer靠谱，完全开源，于是我花了半年的时间将他们集成，如下图

![图片](https://github.com/user-attachments/assets/16e47247-b86d-45ff-ba90-8c66130be223)


这个设计有几个自己给自己挖的坑

1. 废旧物品怎么摆放上洞洞板是个麻烦

----- 于是我给每个设备都手工制作了支架

2. 逆向设计，如何让播放控制面板尽量简单，我希望音源切换按钮在切换音频的同时，也能切换控制接口让一套播放控制按钮能控制三个控制逻辑和电平都不一样的设备，而且还是纯硬件数字电路实现，避免日后维修找不到程序

------ 于是这个板子我硬生生做了4版本,而且最后一版还带着飞线上阵，好在几乎完整实现了我的预期设想
  
3. 为了实现音频律动猫眼电子管的可视化，又引入了共地问题

------ 好在之前哈曼工作经历让我用了两只2元的音频变压器顺利解决

   ![图片](https://github.com/user-attachments/assets/e71c1d0e-064f-49bd-b22c-a4b5fd377e5b)

当把这套设备最终调通后，非常开心，我对音质的追求并不高，但是每个周末的晚上可以在工作室看着音律的跳动听音乐，是非常惬意的事。

## 天使订单

在给几个老友展示了这个不算漂亮的组合后，他们给我下了两套天使订单，让我在保留这三个组合功能的情况下帮他们做漂亮点。

最初我只想保留纯粹的音乐功能，但是做到一半的时候，我打算加入NAS功能，因为音乐也需要空间来存储，于是我增加了3.5寸硬盘，这个需求带来了12V供电的需求

下图是整个ESC-Player的主要BOM
硬件设计很简单，框图如下，只有两块PCB是定制化设计，其他都是标准品，淘宝可买到
![图片](https://github.com/user-attachments/assets/419fbf44-5d53-445a-84eb-3d71f854eea2)

**背板**：为了给3.5寸硬盘供电，在电源部分我选择了Type C输入，然后用诱骗芯片CH224K诱骗出12V，电容滤波后直接给硬盘和次级5V DCDC供电，所以供电只需要很常见的能12V输出的Tpyp C适配器即可
![图片](https://github.com/user-attachments/assets/4f5469ae-cab2-4d05-a80e-1c5eaa874ea1)
**按键板**：承载5个键盘按键和两个编码器旋钮
![图片](https://github.com/user-attachments/assets/619afebf-1cd2-4c34-b6ec-a3985d0a4673)

背板和按键板之间是IO直连的，总计5 key+2x2 Encoder = 9 IO

结构设计也不复杂，

胡桃木板作为底座基板，下面背挂3.5寸硬盘，上面承接亚克力支架
![图片](https://github.com/user-attachments/assets/887ec264-477b-4f54-a75e-8023f442554c)
![图片](https://github.com/user-attachments/assets/a9201f70-c16a-4d9b-a21b-c320d3aef142)

亚克力板做支架，承接树莓派和屏幕
![图片](https://github.com/user-attachments/assets/a2b20a2c-710e-4c06-9daa-7cb759d2a8f7)

这两部分的设计图纸都可以在开源资料里找到，从BOM成分上看，DIY的部分成本大概在400不到，其他的标准品占成本大头

## 功能介绍
接下来介绍一下ESC-Player的功能，下面的MindMap
![图片](https://github.com/user-attachments/assets/7730ef39-3451-48c7-8a32-1daf2f16824a)

主要两大功能，音乐播放器和家用NAS，围绕两大功能分别介绍一下的特点，改良的我也重点介绍一下

**音乐播放器**

大部分常用音源都调通了：网络收音机（需要自己添加频道，很容易），本地音乐，CD碟，Airplay（ Picoreplay 自带shairport能用作airplay串流只支持有线输出，为了能让其输出的蓝牙音箱也能被airplay串流，加入了自定义修改）

Picoreplayer自带的律动频谱和UV表非常多，大家可以有很大的选择空间

![图片](https://github.com/user-attachments/assets/dffd5ed8-f579-4c8e-985b-cd7c5801a5b3)


**NAS**：
NAS基本上都是在原本只做文件服务共享的基础上加上了影音服务，同时把我专辑NAS里使用率最高的功能也移植了过来
![图片](https://github.com/user-attachments/assets/68107e28-f943-48d2-85d7-acf70b1425fa)


1. Filebrowser，可以用网页浏览器管理文件，免去临时使用时不需要映射网络硬盘

2. Alist + Rclone + 自定义Python（开源）：网盘内容后台下载，只需要在手机网盘客户端（如百度网盘）上将想下载的文件放到指定文件夹，即可触发自动拉取到本地硬盘，实现后台下载（功率10W）

3. 编译适配ifuse+simple-mtpfs加上自定义的python（开源）实现iphone/DJI osmo/Gopro相册一键下载到NAS指定文件夹（可增量下载）
![图片](https://github.com/user-attachments/assets/680c4fee-c9e5-4261-9066-066c03463779)

5. Jellyfin适配，网页或者手机客户端可实现看片自由
![图片](https://github.com/user-attachments/assets/628795ef-3d84-4919-8772-33326495b787)

7. Navidrome适配，可在手机上自由自在听NAS里的本地音乐
![图片](https://github.com/user-attachments/assets/d064c949-a416-40b4-9023-757f5092d8af)

当时为了远程SSH support我的朋友做一些问题修复，我部署了frpc，可以在网页上一键打开或关闭远程访问，这必然也是一个安全隐患，欢迎大家审查代码，我只是FRPC的使用者

**其他开发中的功能**

公网访问：适配DDNS动态域名IP更新，带公网IP的家庭网络配合域名（一年30左右）可实现广域网访问，可在任何地点访问个人NAS服务

NFC选歌：通过NFC刷卡的方式调出专辑，让选专辑实现实体化

#
**以上就是ESC-Player的主要功能，所有的源码都是python+shell编写，未编译未加密运行，镜像放在百度网盘**
![图片](https://github.com/user-attachments/assets/09451c24-91bc-473c-8639-d3affb0ce967)

欢迎大家Copy使用，我也会持续开发一些实用的功能，让他释放出更多的能力

欢迎关注我B站账号ZhouYousong，后续有陆续出视频说明。如遇到问题的可以加我wx：zhou-yousong。也欢迎有兴趣量产的朋友联系合作
