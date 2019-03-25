# 组装

材料：

2020欧标铝型材7根（410mm一根，385mm两根，310mm两根，246mm两根）

M5螺钉（8MM长）20个

M5 T型螺母20个

2020欧标铝型材角码12个

工具：

M5内六角扳手

直尺

---
## x轴
1、材料准备
prusa i3非标件一套（这个可以从某宝购买）

M4螺钉8个（10mm长）

M4 T型螺母8个

M3螺钉8个（16mm长）

M3螺钉1个（35mm长）

M3螺母9个

M5螺钉一个（25mm长）

M5螺母一个

两个垫圈

内径5mm的普通轴承一个

T型丝杆螺母2个（M8）

限位开关1个

直线轴承7个（LM8UU）

光轴2根（长340mm）

扎带若干

---
# z轴
1、材料
M4螺钉8个（长10mm）

M4 T型螺母

打印件一套

联轴器2个

光轴2两根（长340mm）

丝杆两根（粗8mm）

42步进电机3个

M3螺钉11个（长8mm）

---
## Y轴
1、材料准备
3D打印件一套

M3螺钉4个（长8mm）

M3螺钉8个（长10mm）

M3螺钉1个（长16mm）

M3螺母9个

M4螺钉8个（长10mm）

M4 T型螺母8个

M5螺钉4个（长10mm）

M5 T型螺母4个

M5螺钉1个（长25mm）

M5螺母1个

光轴2根（长385mm）

直线轴承3个（LM8UU）

铝基板1块

轴承1个（内径5mm）

垫圈2个

限位开关1个

42步进电机一个

扎带若干

---

1、材料
MK8挤出机1套

42步进电机1个

加热铝块1个

喉管1个

挤出头1个

风扇2个：热端冷却风扇（40*40*10建议 Sunon's MF40100V1-1000U-G99）



散热铝片1个

风扇罩1个

电机固定座1个

M3螺钉2个（长14mm）

M3螺钉2个（长8mm）

M3螺母4个

---

热床1个

M3螺钉4个（35mm）

M3螺母4个

弹簧4个

加热棒1个

热敏电阻2个

12v20A电源1个

耐热胶带

-----

### ubuntu octoPrint
- 安装octoPrint
```
运行sudo python setup.py install
```
如果报错执行下两步
- 安装pip
- 安装setuptools
- 配置octoPrint
```
#跟着web设置向导走
```
- 设置端口权限
```
lsusb #查看ardiuno是否挂载
sudo chmod 777 /dev/ttyACM0
```

### 常见问题
1. 电源接反后果：
   - Ramps1.6的SMD poly fuses(保险丝，f1,f2)烧毁
   - merge2560的保险丝旁的MOSFETs()和电压调节器，Protection Diode（反极性二极管）

###
and this on we'll take a look at auto bed leveling and some of the sensors. you can use to get it all working out of bed leveling and marlin is great when you get it set up correctly there's a couple different types of sensor you can use to enable this feature in this video we'll be using an inductive type sensor and a BL touch type sensor 
you can also use a capacitive sensor or even a micro switch and the setup would be about the same for this setup we'll be using my Prusa clone because it already has 
an inductive type sensor installed and a print and z build 
plate.first let's take a look at the specs on these sensors to getan idea of what we're dealing with inductive sensors come in all shapes and sizes a lot of these sensors will only operate in between 6 and 36 volts DC .
the typical 3d printer board only puts out 5 volts ,if you 
have a 6 to 36 volt sensor that won't operate at 5 volts,you can add some resistors and directly cable it to the 12 volt power supply on the prusik load i went with this 5 volt sensor that could be powered by a regular ramp sport i'll put a link to this sensor in the description below.
when you're shopping around for inductive type sensors you're gonna notice there's NPN and PNP type sensors.NPN 
are trggered when you go to ground,PNP are trigggered when 
you go to a positive voltage ,this can be controlled in marlin by switching the in stop setting , so it doesn't really matter which one you choose, for this project ,i'm 
using an NPN type.the first thing you should do is mount 
your sensor .there's a lot of different mounts available on Thingiverse to fit almost every type of printer.the prusik alne already has a spot for the sensor .so we're jst going to use that russo,recommends starting with the sensor around the width of azip tie close to the bed .I found somewhere around one millimeter is about perfect .depending on the sensor you may need to adjust it up or down . now for the wiring .an a standard ramps board these are pretty easy to set up,if you havge a 5 volt sensor you can cable it directly to the zi-in stop ,I found an a lot of these sensors the brown wire is positive the blue wires negative and the black wire is signal.it can be different from sensitive sensor ,so make sure to check the label .
if you don't have a standard grants board maybe somthing like this ,and you can still edit the marlin from where.
you could more than likely still use the sensor ,you'll have to cable the ground and the signal wire to the negative  z n stop ,and then find power in another location .again you can use 12 volt power ,if you add some resistors .on the BL touch you'll notice there's a couple of extra wires .the brown red and orange wire to control the motion of the sensor .while the black and white wire are your z-end stop signal and ground .the brown wire will go to the negative .the red wire will go five volt positi ve and the orange will go to the control signal ,the white 
wire will go to the z-endstop signal and the black wire go the z-endstop negative .when you set up the BLtouch ,it'll have to be configured to be able to control the pop in and 
pop out of the pin .also note when mounting BLtouch,there's a specific height that it needs to be at.consult the BLtouch manual to figure out the perfect height again there'a lot of mounts available for the BLtouch probably for your printer on Thingiverse. remember the inductive type sensor has to have something metal on the bed for you to use it ,the print and z build plate has a thin layer of copper inside it that allows it to work.you can also use an aluminum build plate with some glue stick on it ,but you can't use a glass sheet with aluminum tape on it .so what type sensor should you go with .well if you have a 
metal build plate i definitely go with an inductive type sensor .these can be had for less than three dollars us on Aliexpress and they're very accurate .if you want to print on glass or some other type of material .go with a BLtouch sensor .they're kind of expensive ,but they're also very accurate .now that we know a little bit about the sensors 
how to mount them and how to wire them .let's get into Marlin and see how to configure it.





我们将看看自动床调平和一些传感器。 你可以使用它来完成所有工作的床铺平整。当你正确设置马林鱼是很好的有几种不同类型的传感器。 您可以使用此功能启用此功能，在此视频中我们将使用电感式传感器和BL触摸式传感器。
您也可以使用电容式传感器，甚至微型开关，设置与此设置大致相同，我们将使用我的Prusa克隆，因为它已经安装了感应式传感器并且打印和z构建 请先看看这些传感器的规格，了解我们处理各种形状和尺寸的电感式传感器的问题，很多这些传感器只能工作在6到36伏DC之间。如果你的话，典型的3D打印机板只能输出5伏电压
有一个6到36伏的传感器，不能在5伏电压下运行，你可以添加一些电阻，并直接将它连接到prusik负载上的12伏电源，我使用这个5伏传感器可以通过常规斜坡供电运动我会在下面的描述中提供这个传感器的链接。
当你在购买感应式传感器时，你会发现有NPN和PNP型传感器.NPN
当你去地面时，它们会被踩踏，PNP会被触发
你转到正电压，这可以通过切换停止设置在马林鱼中控制，所以你选择哪一个并不重要，对于这个项目，我是
使用NPN类型。你应该做的第一件事是mount
您的传感器.Thingiverse上有许多不同的安装座可以安装几乎所有类型的打印机。检测器已经有了传感器的位置。所以我们要使用那个russo，建议从宽度周围的传感器开始靠近床的azip领带。我发现大约一毫米左右的地方是完美的。根据传感器你可能需要向上或向下调整。现在用于布线。一个标准的斜坡板这些很容易设置，如果你有一个5伏的传感器，你可以直接连接到zi-in停止，我发现很多这些传感器棕色线是积极的蓝色导线为负极，黑色导线为信号。可能与敏感传感器不同，因此请务必检查标签。
如果你没有标准的补助板可能是这样的东西，你仍然可以从哪里编辑马林鱼。
您可能仍然可能仍然使用传感器，您必须将地线和信号线连接到负zn光阑，然后在另一个位置找到电源。如果添加一些电阻，则可以使用12伏电源。在BL触摸上你会注意到有一些额外的电线。棕色的红色和橙色的电线来控制传感器的运动。而黑色和白色的电线是你的z端停止信号和地面。棕色的电线将会去负极。红线将位​​于5伏位置，橙色将转向控制信号，白色
导线将转到z-endstop信号，黑色导线变为z-endstop负极。当你设置BLtouch时，它必须被配置为能够控制弹出和
弹出BLtouch，还有一个特定的高度需要处理。请查看BLtouch手册，再次找出完美的高度，可以为Thingiverse上的打印机提供很多可用的BLtouch支架。 。请记住，感应式传感器必须在床上放置金属物才能使用它，打印和z构建板内部有一层薄薄的铜层，可以让它工作。你也可以使用带有胶水的铝制底板坚持下去，但你不能使用带铝带的玻璃板。那么你应该选择什么类型的传感器。如果你有
金属底板我肯定会使用感应式传感器。在Aliexpress上我们的价格可以低于三美元而且它们非常准确。如果你想在玻璃或其他类型的材料上打印。使用BLtouch传感器它们有点贵，但它们也非常准确。现在我们对传感器有一点了解
如何安装它们以及如何连接它们.let进入Marlin并看看如何配置它。