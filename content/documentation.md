## 前言
Map.Design 服务完全兼容mapbox SDK，基于mapbox-gl-js可以构建用于在网页端展示地图的应用。

## 使用教程

### 添加依赖
在 html 文件的 header 标签中添加：
```html
<link href='https://mapdesign.oss-cn-beijing.aliyuncs.com/code/js/mapbox-gl.css' rel='stylesheet' />
<script src='https://mapdesign.oss-cn-beijing.aliyuncs.com/code/js/mapbox-gl.js'></script>
```
以上sdk组件由mapbox-gl-js修改而来，详细代码：[https://github.com/tomapto/mapbox-gl-js](https://github.com/tomapto/mapbox-gl-js)

### 引入相关 CSS 样式
首先，在 header 的标签中添加相关的样式：
```html
<style>
html, body, #map {
width: 100%;
height: 100%;
margin: 0;
padding: 0;
}
#map {
position: absolute;
top: 0;
bottom: 0;
}
.shadow {
box-shadow: 0 0 25px 0 rgba(0,0,0,0.15);
}
.round-bottomleft {
border-bottom-left-radius: 3px;
}
.mapboxgl-ctrl-nav > a {
border-color: rgba(0,0,0,.1);
}
@media only screen and (max-width:640px) {
.leaflet-left .leaflet-control,
.mapboxgl-ctrl-top-left .mapboxgl-ctrl {
margin-top: 70px;
}
.round-bottomleft {
border-bottom-left-radius: 0;
}
.mobile-fullwidth {
width: 100%;
height: 60px;
overflow: auto;
}
}
</style>
```

### 地图 html 元素
在 body 标签中，添加下面的标签
```html
<div id='map'></div>
```

### 添加浏览器支持判断
然后，在 body 的 script 标签中，添加相关浏览器代码：
```javascript
if ( mapboxgl.supported() ) {
// 添加相关渲染方法
renderMapboxGL();
} else {
document.getElementById("map").innerText="您的浏览器版本较低，请升级浏览器(IE11以上，或下载最新chrome浏览器)";
}
```

### 渲染方法 

我们新建一个 renderMapboxGL 的方法：

```javascript
function renderMapboxGL() {
}
```

### 配置 token
首先，打开 Map.Design 密钥页面，点击复制按钮获取到 [默认密钥](https://www.map.design/#/dashboard/account/tokens)。
然后，在 renderMapboxGL 方法中添加下面的方法
```
mapboxgl.accessToken = <默认密钥>；
```

### 配置 API_URL
```javascript
mapboxgl.config.API_URL = 'https://www.map.design';
```

### 创建地图
首先，打开[样式集列表](https://www.map.design/#/dashboard/stylesets)，找到想要展示的样式，点击更多按钮，点击复制，获取到对应 URL 路径；
```javascript
window.map = new mapboxgl.Map({
container: 'map', //对应的 html 元素 ID
style: <样式对应的 URL 路径>,
hash: true,
scrollZoom: true
}).addControl(new mapboxgl.NavigationControl(), 'top-left');
```

### 完整代码

下面是创建地图的完整代码：

```html
<!DOCTYPE html>
<html>
<head>
<meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
<meta charset='utf-8' />
<title>standard_siwei | Map.Design</title>

<link href='https://mapdesign.oss-cn-beijing.aliyuncs.com/code/js/mapbox-gl.css' rel='stylesheet' />
<script src='https://mapdesign.oss-cn-beijing.aliyuncs.com/code/js/mapbox-gl.js'></script>

<style>
html, body, #map {
width: 100%;
height: 100%;
margin: 0;
padding: 0;
}
#map {
position: absolute;
top: 0;
bottom: 0;
}
.shadow {
box-shadow: 0 0 25px 0 rgba(0,0,0,0.15);
}
.round-bottomleft {
border-bottom-left-radius: 3px;
}
.mapboxgl-ctrl-nav > a {
border-color: rgba(0,0,0,.1);
}
@media only screen and (max-width:640px) {
.leaflet-left .leaflet-control,
.mapboxgl-ctrl-top-left .mapboxgl-ctrl {
margin-top: 70px;
}
.round-bottomleft {
border-bottom-left-radius: 0;
}
.mobile-fullwidth {
width: 100%;
height: 60px;
overflow: auto;
}
}
</style>
</head>
<body>
<div id='map'></div>
<script>
(function() {
'use strict';

if ( mapboxgl.supported() ) {
renderMapboxGL();
} else {
document.getElementById("map").innerText="您的浏览器版本较低，请升级浏览器(IE11以上，或chrome浏览器)";
}

function renderMapboxGL(options) {
mapboxgl.accessToken = <获取到的token>;
mapboxgl.config.API_URL = 'https://www.map.design';

window.map = new mapboxgl.Map({
container: 'map',
style: <对应的样式地址>,
hash: true,
scrollZoom: true
}).addControl(new mapboxgl.NavigationControl(), 'top-left');
}
})();
</script>
</body>
</html>
```

## 相关文档
更多 API 用法，请参考( [Mapbox 官方文档](https://www.mapbox.com/mapbox-gl-js/api/) )