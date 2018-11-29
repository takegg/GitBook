# 移动端dpr适配

## 全局js
- scale.js
```js
(function (win, doc) {
  var docEl = doc.documentElement // 文档
  let maxwidth = 640 // 最大宽度
  let dpr = devicePixelRatio === 4 ? 1 : devicePixelRatio // 像素比
  let scale = 1 / dpr // 缩放率
  let tid
  docEl.dataset.dpr = dpr// 设置data-*属性，这里设置data-dpr属性
  window.dpr = dpr

  /**
 * 创建并设置视口缩放级
 * **/
  var metaEl = doc.createElement('meta')
  metaEl.name = 'viewport'
  metaEl.content = setScale(scale)

  docEl.firstElementChild.appendChild(metaEl) // 将设置视口缩放插入头部
  let designScale = (docEl.dataset.width || 1080) / 100 // 转化设计稿缩小100倍(约定设计稿是1080px)

  /**
 * 测量页面1rem的px值（在头部插入div）
 * **/
  var h = document.getElementsByTagName('head')[0]
  let d = document.createElement('div')
  d.style.width = '1rem'
  d.style.display = 'none'
  h.appendChild(d)
  var rootfs = parseFloat(getComputedStyle(d, null).getPropertyValue('width'))// 获取浏览器计算后的1rem的px（值测量元素宽度），并取整
  alert(rootfs)

  /**
 * 设置根字体大小
 *
 * **/
  var refreshRem = function () {
    var width = document.documentElement.clientWidth// 文档宽度
    if (width / dpr > maxwidth) {
      width = maxwidth * 1
    }
    // docEl.style.fontSize = width / designScale + 'px'
    docEl.style.fontSize = width / designScale / rootfs * 100 + '%'// 设置后页面单位为相对大小
  }

  refreshRem()

  /**
设置mate
**/
  function setScale (scale) {
    return 'width=device-width,initial-scale=' + scale + ',maximum-scale=' + scale + ',minimum-scale=' + scale
  }

  /**
窗口变化触发
**/
  win.addEventListener('resize', function () {
    clearTimeout(tid)
    tid = setTimeout(refreshRem, 300)
  }, false)

  /**
浏览器前进后退时触发pageshow
**/
  win.addEventListener('pageshow', function (e) {
    if (e.persisted) {
      clearTimeout(tid)
      tid = setTimeout(refreshRem, 300)
    }
  }, false)

  /**
dom加载
**/
  win.addEventListener('DOMContentLoaded', function (e) {
    var body = document.getElementsByTagName('body')[0]
    body.className = 'dpr' + Math.floor(dpr)
    body.style.maxWidth = designScale + 'rem'
    body.style.margin = '0 auto'
  }, false)
})(window, document)

```
## 第二步：转换px为erm，相对根元素大小
> 安装postcss-pxtorem转换插件
> 
> 配置此插件
.postcssrc.js
 ```js
 // https://github.com/michael-ciniawsky/postcss-load-config
 module.exports = {
  "plugins": {
    "postcss-import": {},
    "postcss-url": {},
    // to edit target browsers: use "browserslist" field in package.json
    "autoprefixer": {},
    "postcss-pxtorem": {
      rootValue: 100,//相对值
      selectorBlackList: ["vux", "scroller-", "weui", "dp-"],//忽略的前缀
      propList: ['*']//要转换的
    }
  }
}
 ```