品微公司前端代码片段
==
###CSS代码
######禁用IOS系统下输入框控件默认样式
```html
-webkit-appearance: none;
```
######启用IOS系统下原生滚动效果
    -webkit-overflow-scrolling: touch;
######禁止元素被选中
    -webkit-user-select: none;-webkit-touch-callout: none;
######禁止图片被选中（App内置webview）
    pointer-events: none;
######文字强制不换行并超出父元素宽度多余字以省略号显示
    overflow: hidden;white-space: nowrap; text-overflow:ellipsis;
######webkit内核浏览器滚动条元素
    ::-webkit-scrollbar{}
###JS代码
######JS打乱数组最高效的方法
```js
var arr=[];
for(var i=0;i<100;i++){
        arr[i]=i;
    }
arr.sort(function(){ return 0.5 - Math.random() })
var str=arr.join();
alert(str);
```
######JS上传图片及时预览
```js
var f = document.getelementbyid('upload').files[0];
var src = window.URL.createObjectURL(f);
document.getElementById('preview').src = src;
```
######禁止移动端页面滚动
```js
//原生js方式
document.body.addEventListener('touchmove', function(event) {
	event.preventDefault();
}, false);
//jQuery方式
$("body").on('touchmove', function(event) {
    event.preventDefault();
});
//如果页面有逻辑需要,先禁止滚动，然后取消禁止滚动，建议用jQuery方式，取消禁止滚动代码如下
$("body").off('touchmove');
```
######阿里云调用wxjsapi方式
```js
$.ajax({
    dataType : 'jsonp',
    url      : "http://slib.sinaapp.com/wxjsapi.php?action=token",
    data     : {"url":window.location.href.split('#')[0]},
    async    : true,
    success  : function (data) {
        var key = data;
        wx.config({
            debug     : false,
            appId     : key.appId,
            timestamp : key.timestamp,
            nonceStr  : key.nonceStr,
            signature : key.signature,
            jsApiList : ['onMenuShareTimeline','onMenuShareAppMessage','onMenuShareQQ','onMenuShareWeibo','startRecord','stopRecord','onVoiceRecordEnd','playVoice','pauseVoice','stopVoice','onVoicePlayEnd','uploadVoice','downloadVoice','chooseImage','previewImage','uploadImage','downloadImage','translateVoice','getNetworkType','openLocation','getLocation','hideOptionMenu','showOptionMenu','hideMenuItems','showMenuItems','hideAllNonBaseMenuItem','showAllNonBaseMenuItem','closeWindow','scanQRCode','chooseWXPay','openProductSpecificView','addCard','chooseCard','openCard']
        });
		wx.ready(function(){
            //do something
	    });
    }
});
```
######新浪云调用wxjsapi方式
```js
$.ajax({
    type    : "post",
    url     : "/wxjs.php?action=token",
    data    : {"url": window.location.href.split('#')[0]},
    async   : true,
    success : function (data) {
        var key = JSON.parse(data);
        wx.config({
            debug     : false,
            appId     : key.appId,
            timestamp : key.timestamp,
            nonceStr  : key.nonceStr,
            signature : key.signature,
            jsApiList : ['onMenuShareTimeline','onMenuShareAppMessage','onMenuShareQQ','onMenuShareWeibo','startRecord','stopRecord','onVoiceRecordEnd','playVoice','pauseVoice','stopVoice','onVoicePlayEnd','uploadVoice','downloadVoice','chooseImage','previewImage','uploadImage','downloadImage','translateVoice','getNetworkType','openLocation','getLocation','hideOptionMenu','showOptionMenu','hideMenuItems','showMenuItems','hideAllNonBaseMenuItem','showAllNonBaseMenuItem','closeWindow','scanQRCode','chooseWXPay','openProductSpecificView','addCard','chooseCard','openCard']
        });
        wx.ready(function(){
            //do something
        });
    }
});
```
######微信推送抓取视频地址程序(单个视频)
```js
//使用方法：用chrome打开推送链接，按F12（windows系统）调出开发者工具，将如下代码复制粘贴到console控制台即可
var url = document.getElementsByTagName("iframe")[0].getAttribute("data-src").split("?")[1];
var reg = new RegExp("(^|&)vid=([^&]*)(&|$)");
var r = url.match(reg);
window.open("http://v.qq.com/page/"+ decodeURIComponent(r[2]) +".html");
```
###HTML代码
######调用微信WebView内置图片查看功能
```html
<!--YourImageURL为全地址-->
<a href="weixin://viewimage/`YourImageURL`">AnyThing</a>
```
######HTML头部标签
```html
<!DOCTYPE html> <!-- 使用 HTML5 doctype，不区分大小写 -->
<html lang="zh-cmn-Hans"> <!-- 更加标准的 lang 属性写法 http://zhi.hu/XyIa -->
<head>
    <!-- 声明文档使用的字符编码 -->
    <meta charset='utf-8'>
    <!-- 优先使用 IE 最新版本和 Chrome -->
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/>
    <!-- 页面描述 -->
    <meta name="description" content="不超过150个字符"/>
    <!-- 页面关键词 -->
    <meta name="keywords" content=""/>
    <!-- 网页作者 -->
    <meta name="author" content="name, email@gmail.com"/>
    <!-- 搜索引擎抓取 -->
    <meta name="robots" content="index,follow"/>
    <!-- 为移动设备添加 viewport -->
    <meta name="viewport" content="initial-scale=1, maximum-scale=3, minimum-scale=1, user-scalable=no">
    <!-- `width=device-width` 会导致 iPhone 5 添加到主屏后以 WebApp 全屏模式打开页面时出现黑边 http://bigc.at/ios-webapp-viewport-meta.orz -->

    <!-- iOS 设备 begin -->
    <meta name="apple-mobile-web-app-title" content="标题">
    <!-- 添加到主屏后的标题（iOS 6 新增） -->
    <meta name="apple-mobile-web-app-capable" content="yes"/>
    <!-- 是否启用 WebApp 全屏模式，删除苹果默认的工具栏和菜单栏 -->

    <meta name="apple-itunes-app" content="app-id=myAppStoreID, affiliate-data=myAffiliateData, app-argument=myURL">
    <!-- 添加智能 App 广告条 Smart App Banner（iOS 6+ Safari） -->
    <meta name="apple-mobile-web-app-status-bar-style" content="black"/>
    <!-- 设置苹果工具栏颜色 -->
    <meta name="format-detection" content="telphone=no, email=no"/>
    <!-- 忽略页面中的数字识别为电话，忽略email识别 -->
    <!-- 启用360浏览器的极速模式(webkit) -->
    <meta name="renderer" content="webkit">
    <!-- 避免IE使用兼容模式 -->
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <!-- 针对手持设备优化，主要是针对一些老的不识别viewport的浏览器，比如黑莓 -->
    <meta name="HandheldFriendly" content="true">
    <!-- 微软的老式浏览器 -->
    <meta name="MobileOptimized" content="320">
    <!-- uc强制竖屏 -->
    <meta name="screen-orientation" content="portrait">
    <!-- QQ强制竖屏 -->
    <meta name="x5-orientation" content="portrait">
    <!-- UC强制全屏 -->
    <meta name="full-screen" content="yes">
    <!-- QQ强制全屏 -->
    <meta name="x5-fullscreen" content="true">
    <!-- UC应用模式 -->
    <meta name="browsermode" content="application">
    <!-- QQ应用模式 -->
    <meta name="x5-page-mode" content="app">
    <!-- windows phone 点击无高光 -->
    <meta name="msapplication-tap-highlight" content="no">
    <!-- iOS 图标 begin -->
    <link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-57x57-precomposed.png"/>
    <!-- iPhone 和 iTouch，默认 57x57 像素，必须有 -->
    <link rel="apple-touch-icon-precomposed" sizes="114x114" href="/apple-touch-icon-114x114-precomposed.png"/>
    <!-- Retina iPhone 和 Retina iTouch，114x114 像素，可以没有，但推荐有 -->
    <link rel="apple-touch-icon-precomposed" sizes="144x144" href="/apple-touch-icon-144x144-precomposed.png"/>
    <!-- Retina iPad，144x144 像素，可以没有，但推荐有 -->
    <!-- iOS 图标 end -->

    <!-- iOS 启动画面 begin -->
    <link rel="apple-touch-startup-image" sizes="768x1004" href="/splash-screen-768x1004.png"/>
    <!-- iPad 竖屏 768 x 1004（标准分辨率） -->
    <link rel="apple-touch-startup-image" sizes="1536x2008" href="/splash-screen-1536x2008.png"/>
    <!-- iPad 竖屏 1536x2008（Retina） -->
    <link rel="apple-touch-startup-image" sizes="1024x748" href="/Default-Portrait-1024x748.png"/>
    <!-- iPad 横屏 1024x748（标准分辨率） -->
    <link rel="apple-touch-startup-image" sizes="2048x1496" href="/splash-screen-2048x1496.png"/>
    <!-- iPad 横屏 2048x1496（Retina） -->

    <link rel="apple-touch-startup-image" href="/splash-screen-320x480.png"/>
    <!-- iPhone/iPod Touch 竖屏 320x480 (标准分辨率) -->
    <link rel="apple-touch-startup-image" sizes="640x960" href="/splash-screen-640x960.png"/>
    <!-- iPhone/iPod Touch 竖屏 640x960 (Retina) -->
    <link rel="apple-touch-startup-image" sizes="640x1136" href="/splash-screen-640x1136.png"/>
    <!-- iPhone 5/iPod Touch 5 竖屏 640x1136 (Retina) -->
    <!-- iOS 启动画面 end -->

    <!-- iOS 设备 end -->
    <meta name="msapplication-TileColor" content="#000"/>
    <!-- Windows 8 磁贴颜色 -->
    <meta name="msapplication-TileImage" content="icon.png"/>
    <!-- Windows 8 磁贴图标 -->

    <link rel="alternate" type="application/rss+xml" title="RSS" href="/rss.xml"/>
    <!-- 添加 RSS 订阅 -->
    <link rel="shortcut icon" type="image/ico" href="/favicon.ico"/>
    <!-- 添加 favicon icon -->

    <title>标题</title>
</head>
```
