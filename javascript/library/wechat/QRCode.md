# 扫码

## 示例代码
```js
<html>
<head>
<title>Welcome to nginx!</title>
<script
  src="https://code.jquery.com/jquery-1.12.4.min.js"
  integrity="sha256-ZosEbRLbNQzLpnKIkEdrPv7lOy9C27hHQ+Xp8a4MxAQ="
  crossorigin="anonymous"></script>
<script src="http://res.wx.qq.com/open/js/jweixin-1.2.0.js"></script>  
  
<script>
$(document).ready(function(){
    $.ajax(
	{url:"http://scrm-h5-dev.vivo.com.cn/jsapi/getCpJsapiConfig?url=http%3A%2F%2Fscrm-h5-dev.vivo.com.cn%2F",
	 dataType: "json",
	 success:function(result){
		
        alert(JSON.stringify(result));
		wx.config({
			debug: true, // 开启调试模式,调用的所有api的返回值会在客户端alert出来，若要查看传入的参数，可以在pc端打开，参数信息会通过log打出，仅在pc端时才会打印。
			appId: result['data']['appId'], // 必填，公众号的唯一标识
			timestamp: result['data']['timestamp'] , // 必填，生成签名的时间戳
			nonceStr: result['data']['nonceStr'], // 必填，生成签名的随机串
			signature: result['data']['signature'],// 必填，签名，见附录1
			jsApiList: result['data']['jsApiList'] // 必填，需要使用的JS接口列表，所有JS接口列表见附录2
		});
		wx.ready(function(){
			
			wx.scanQRCode({
                // 默认为0，扫描结果由微信处理，1则直接返回扫描结果
                needResult : 1,
                desc : 'scanQRCode desc',
                success : function(res) {
                    //扫码后获取结果参数赋值给Input
                    var url = res.resultStr;
                    alert(url);
                }
            });
		});
		/*
		wx.chooseImage({
			  count: 1, // 默认9
			  sizeType: ['original', 'compressed'], // 可以指定是原图还是压缩图，默认二者都有
			  sourceType: ['album', 'camera'], // 可以指定来源是相册还是相机，默认二者都有
			  success: function (res) {
				// 返回选定照片的本地文件路径列表，tempFilePath可以作为img标签的src属性显示图片
				var tempFilePaths = res.tempFilePaths;
				alert(res);
			  }
			})
		*/
		
    }});
});
</script>
</head>
<body>

<p>If you click on me, I will disappear.</p>
<p>Click me away!</p>
<p>Click me too!</p>

</body>
</html>
</html>

```