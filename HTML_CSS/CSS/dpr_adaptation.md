# 移动端dpr适配

## 全局js
- scale.js
```js
(function (win, doc) {
  var docEl = doc.documentElement,// 文档
    maxwidth = 640,//最大宽度
    dpr = devicePixelRatio == 4 ? 1 : devicePixelRatio,//像素比
    scale = 1 / dpr,//缩放率
    tid
  docEl.dataset.dpr = dpr;//设置data-*属性，这里设置data-dpr属性
  window.dpr = dpr;

/**
 * 创建并设置视口缩放级
 * **/
  var metaEl = doc.createElement('meta')
  metaEl.name = 'viewport'
  metaEl.content = setScale(scale)

  docEl.firstElementChild.appendChild(metaEl) // 将设置视口缩放插入头部
  var design_scale = (docEl.dataset.width || 1080) / 100 // 转化设计稿缩小100倍

/**
 * 测量页面1rem的px值（在头部插入div）
 * **/
  var h = document.getElementsByTagName('head')[0],
    d = document.createElement('div')
  d.style.width = '1rem'
  d.style.display = 'none'
  h.appendChild(d)
  var rootfs = parseFloat(getComputedStyle(d, null).getPropertyValue('width'))//获取浏览器计算后的测量元素宽度px值，并取整

/**
 * 设置根字体大小
 * 
 * **/
  var refreshRem = function () {
    var width = document.documentElement.clientWidth//文档宽度
    if (width / dpr > maxwidth) {
      width = maxwidth * 1
    }
    // docEl.style.fontSize = width / design_scale + 'px';
    docEl.style.fontSize = width / design_scale / rootfs * 100 + '%'
    // docEl.style.fontSize = width / design_scale / rootfs * 100 * dpr + '%'
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
    body.className = 'dpr' + Math.floor(dpr);
    body.style.maxWidth = design_scale + 'rem'
    body.style.margin = '0 auto'
  }, false)

})(window, document)

```