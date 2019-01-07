# 配置

<a href='https://reprap.org/wiki/Calibration'>原文</a>

## PLA
### 层高
> 层高<80%喷嘴直径，基础宽度>=喷嘴直径。你可以降低层高或增大基础宽度。层高没有硬性下限（它受限于您在非常低的流速下保持流量一致的能力）。
> 有文章推荐：建议层高0.2毫米，挤压宽度0.5毫米，无论他使用哪个喷嘴。
> Slic3r会根据您的喷嘴直径自动为您选择挤出宽度。

### 温度
> 以5摄氏度的幅度调试
> 
```
PLA
Hotend: 185 °C
Bed: 60 °C

ABS
Hotend: 230 °C
Bed: 110 °C
```

## 理论和数学
### X,Y轴
>可以通过轨道偏移和整体缩放来校准。如图<br/>
<img width='640px' src='https://reprap.org/mediawiki/images/0/0f/RepRap_Calibration_Frame_Drawing.png'>
### Z轴
>可使用在线工具<a href='https://www.prusaprinters.org/calculator/'>计算器</a>计算，修改marlin配置文件的STEPS_PER_MM。

----

# marlin的Configuration.h配置

## 三轴及挤出机单位配置
``` c++
#define DEFAULT_AXIS_STEPS_PER_UNIT {78.7402,78.7402,200*8/3,760*1.1}
#define 默认轴每单位步数 {X轴每单位步数, Y轴每单位步数, Z轴每单位步数, 挤出机每单位步数}

// 皮带轮轴计算
// Steps per Unit (X and Y Axes) = Motor Steps per Revolution / Idler Teeth / Belt Pitch
// 每单位步数 (X、Y轴) = 电机每转的步数 / 空转齿 / 皮带间距

// 螺杆驱动轴计算
// Steps per Unit (Z Axis) = Motor Steps per Revolution / Rod Pitch
// 每单位步数（Z轴）=每转的电机步数/杆节距

// 挤出机
// Steps per Unit (Extruder) = Motor Steps per Revolution * Extruder Gear Ratio / (Pinch Wheel Diameter * Pi)
// 每单位步数（挤出机）=每转的电机步数*挤出机齿轮比/（夹紧轮直径* Pi）
```
> **电机每转步数**：由电机确定的这些方程中的变量是“每电机转速步数”，这是电机进行一次，完整，三百六十度转动所需的步数。
> 对于0.9度步进器，这将是360°/ 0.9°，或400步全步。可是等等！我们还必须考虑微步进 - 这通常以1/8或1/16为增量（Pololu驱动器为1/16）。<br/>
> 
> 因此，400步全程除以1/16微步进将是6400，这表示电机完全旋转所需的微步数。
> 1/16微步进的1.8度电机需要3200微步才能完全旋转。<br/>
> 
> 对于使用1/16微步进，带5mm节距皮带和8齿齿轮的0.9度电机，每单位的步数为：<br/>
> 每转6400步，除以5，除以8，或每单位160步（在这种情况下为毫米）。
> 校准打印件<a href='https://www.matterhackers.com/downloads/AMIfv95Oi1e_KxgpHR5qvGg0uD4sYAWjOH1Hy34erMHY8gQuGkSRoG9xV_XUHXXRmoaR7eGEYvXP8fm4q3_ztNrx0kXYirx9TN9DbPcqoHbURFFGKXwlsKBc_QZTitSYUSmmvXmb-53Lr3Ah6EIgMvVZroW4DZZDYH1lLI_g08NYPJrhIrI3Kvc'>20mm x 20mm x 20mm空心校准立方体</a>
示例：
```
 #define DEFAULT_AXIS_STEPS_PER_UNIT {78.7402,78.7402,200*8/3,760*1.1}

即:

#define STEPS_PER_REVOLUTION_X 3200
#define STEPS_PER_REVOLUTION_Z 3200
#define STEPS_PER_REVOLUTION_E 3200
#define STEPS_PER_REVOLUTION_Y 6400

#define IDLER_TEETH_X 8
#define IDLER_TEETH_Y 8


#define BELT_PITCH_X (.2 * MM_PER_INCH)
#define BELT_PITCH_Y (.2 * MM_PER_INCH)

#define PITCH_OF_Z_ROD 1.25

// makergear extruder box
#define EXTRUDER_GEAR_RATIO 13.0

#define PINCH_WHEEL_DIAMETER 11.59

#define AXIS_STEPS_PER_UNIT_X (STEPS_PER_REVOLUTION_X / IDLER_TEETH_X / BELT_PITCH_X)

#define AXIS_STEPS_PER_UNIT_Y (STEPS_PER_REVOLUTION_Y / IDLER_TEETH_Y / BELT_PITCH_Y)

#define AXIS_STEPS_PER_UNIT_Z ****(STEPS_PER_REVOLUTION_Z / PITCH_OF_Z_ROD)

#define AXIS_STEPS_PER_UNIT_E (STEPS_PER_REVOLUTION_E * EXTRUDER_GEAR_RATIO / (PINCH_WHEEL_DIAMETER * PI))

#define DEFAULT_AXIS_STEPS_PER_UNIT {AXIS_STEPS_PER_UNIT_X, AXIS_STEPS_PER_UNIT_Y, AXIS_STEPS_PER_UNIT_Z, AXIS_STEPS_PER_UNIT_E}
```
><a href="http://calculator.josefprusa.cz/#MotorStuffSPMB">皮带轮计算</a><a href='http://calculator.josefprusa.cz/#MotorStuffSPML'>丝杆计算</a>