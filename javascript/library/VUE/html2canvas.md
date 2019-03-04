# 模拟截图

## 步骤
- 引入html2canvas插件
- 获取dpr
- 获取图片格式
- 将目标html内的获取到的图片src加时间戳参数对（兼容微信）
- 设置目标html内图片交叉源属性为匿名（canvas转data64会有跨域污染）
- 将目标html内的获取到的图片src替换为data64,记得设置清晰度为1，（img.onload在Android微信不兼容）
- 设置html2canvas配置背景透明，缩放dpr，不允许污染，获取base64
- 将最终所得base64赋值给展示截图img
