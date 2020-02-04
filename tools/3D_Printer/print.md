# 打印

## 配置

### samplify3D
2. layer
4. fill
```shell 
General
. Internal Fill Pattern # 内部填充图案,选Honeycomb机械强度好
. External Ffill Pattern # 外部填充图案(顶部，底部)concentric（同心），rectilinear（直线：推荐）
. interior Fill Percentage # 通常20-40，超过50非常密
. outline overlap # 轮廓重叠
External Infill Angle Offsets(顶底填充角度偏移)
. 
```
11. Other
```shell 
Bridging
. unsupported area shreshold # 不支持区域阈值
. Extra inflation distance # 额外的充气距离
. Bridging extrustion multiplier # 桥接挤压倍增器
. 
. Use fixed bridging infill angle # 使用固定的桥接填充角度（默认不勾选）
. Apply bridging settings to perimeters   # 应用拉桥设置到外围,Rectilinear(直线)，Concentric（同心）
. 
```

## 问题
1. 拉桥时风扇满速->热头温度暴降->停机（Printer halted.kill() called!）
* 风扇聚焦喷嘴下方或加热块包裹保温层。验证：待验证
* 调降风扇最大值。验证：待验证。
* aduinoIDE上载代码报报端口错：其他可联接aduino的软件占用端口。


2. 拉桥失败
* 设置支撑。验证：通过
* 设置拉桥：

3. Y轴shift：检查皮带轮螺丝，皮带松紧，设置填充速度（从70%降至40%验证通过）