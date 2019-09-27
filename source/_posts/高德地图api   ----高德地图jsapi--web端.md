# 高德地图api 		<sub>----[高德地图jsapi--web端](https://lbs.amap.com/api/javascript-api/guide/abc/prepare)</sub>

## 引入文件

### 注册账号

1. [注册开发者账号](https://lbs.amap.com/dev/id/newuser)
2. [应用管理]-->[创建新应用]
3. 为应用[添加 Key](https://lbs.amap.com/dev/key/app)，「服务平台」一项请选择「 Web 端 ( JSAPI ) 」

### 准备页面

1.	在页面添加 JS API 的入口脚本标签，并将其中「您申请的key值」替换为您刚刚申请的 key；

[HTML](javascript:void(0);)

```
<script type="text/javascript" src="https://webapi.amap.com/maps?v=1.4.11&key=您申请的key值"></script> 
```

2. 添加`div`标签作为地图容器，同时为该`div`指定`id`属性；

[HTML](javascript:void(0);)

```
<div id="container"></div> 
```

3. 为地图容器指定高度、宽度；

[CSS](javascript:void(0);)

```
#container {width:300px; height: 180px; }  
```

4.	进行移动端开发时，请在`head`内添加`viewport`设置，以达到最佳的绘制性能；

[HTML](javascript:void(0);)

```
<meta name="viewport" content="initial-scale=1.0, user-scalable=no"> 
```

5.	在完成如上准备工作之后便可以开始进行开发工作了，查看快速入门。

## 异步加载 JS API

上一节说明的是最基本的同步加载 JS API 的方式，如果您需要异步加载，比如通过`appendChild`，或者通过`require`等异步方式来加载，这时需要您需要先准备一个全局的回调函数作为 JS API 异步加载的回调函数，并将其函数名作为`callback`参数添加在 JS API 的引用地址后面，此时要注意，回调函数应该在脚本请求发出之前进行声明。异步加载方式只有在回调之后，才能开始调用JSAPI的相关接口。比如

[JavaScript](javascript:void(0);)

```
  window.onLoad  = function(){
        var map = new AMap.Map('container');
  }
  var url = 'https://webapi.amap.com/maps?v=1.4.11&key=您申请的key值&callback=onLoad';
  var jsapi = doc.createElement('script');
  jsapi.charset = 'utf-8';
  jsapi.src = url;
  document.head.appendChild(jsapi);
```

更多的加载方式，请查看「[JS API 的加载](https://lbs.amap.com/api/javascript-api/guide/abc/load)」

### HTTPS 的支持

JSAPI 1.3 开始完全支持 `HTTPS` 协议，如需使用安全协议，替换 JS API 的入口脚本URL中的`http`为`https`即可。随着 Chrome、iOS 等相继限制非安全域的定位请求，我们建议您升级网站到`HTTPS`协议，并使用`HTTPS`协议加载 JS API。

[HTML](javascript:void(0);)

```
<script type="text/javascript" src="https://webapi.amap.com/maps?v=1.4.11&key=您申请的key值"></script> 
```

## 生成地图对象

`map = new Amap.Map('container', mapConfig)`创建地图对象，`container`为页面中需要绑定地图对象的dom元素id。`mapConfig`为关于`map`的配置项。

~~~JavaScript
const mapConfig = {
    zoom: 16, // 地图初始放大级数
    resizeEnable: true, // 是否监控地图容器尺寸变化，默认值为false
    center: [], // LngLat 设置地图中心点坐标
};
~~~

详细配置参考官方文档 ---------> [高德地图api参考手册](https://lbs.amap.com/api/javascript-api/reference/map)

#### 操作地图对象

~~~javascript
// 增加标记点
addMarker(mapMarker) {
    this.AMap = window.AMap;
    const { AMap } = this;
    mapMarker.forEach((element) => { // 经纬度对象数组，标记多个点
        const marker = new AMap.Marker({
            position: new AMap.LngLat(element.lng, element.lat), // 地图函数解析经纬度，也可以直接以[lng, lat]输出
            title: element.entName, // 鼠标悬浮显示文字
            icon: '//a.amap.com/jsapi_demos/static/demo-center/icons/poi-marker-default.png', // 标记显示图标
        });
        if (map.getZoom() > 13) { // getZoom() 获取当前缩放级别
            marker.setLabel({
                offset: new AMap.Pixel(20, 0), // 修改label相对于maker的位置
                content: element.entName, // label显示内容
            });
        }
        map.on('zoomchange', () => { // 监测地图缩放
            if (map.getZoom() <= 13) {
                marker.setLabel('');
            } else {
                marker.setLabel({
                    offset: new AMap.Pixel(20, 0), // 修改label相对于maker的位置
                    content: element.entName,
                });
            }
        });
        this.markerList.push(marker);
    });
    map.add(this.markerList); // 将生成的标点绑定到地图对象中
}
~~~

#### 自定义标点样式

~~~javascript
this.markerList.forEach((element) => {
    if (element.getPosition().lng === item.lng && element.getPosition().lat === item.lat) {
        // 自定义点标记内容
        const markerContent = document.createElement('div');
        markerContent.style = 'position: absolute; width: 19px; height: 33px; opacity: 1;';

        // 点标记中的图标
        const markerImg = document.createElement('img');
        markerImg.style = 'width: 100%; height: 100%;';
        markerImg.className = 'markerlnglat';
        markerImg.src = '//a.amap.com/jsapi_demos/static/demo-center/icons/poi-marker-red.png';
        markerContent.appendChild(markerImg);

        // 点标记中的文本
        const markerSpan = document.createElement('span');
        markerSpan.className = 'marker';
        markerContent.appendChild(markerSpan);
        element.setContent(markerContent); // 更新点标记内容
        //element.setIcon('//a.amap.com/jsapi_demos/static/demo-center/icons/poi-marker-red.png'); // 设置图标样式
        map.setCenter([element.getPosition().lng, element.getPosition().lat]); // 将此经纬度定位到地图中心
        element.setAnimation('AMAP_ANIMATION_DROP'); // 给标记点增加动画效果
    }
});
~~~

#### 地图插件使用

~~~JavaScript
this.map.plugin(['AMap.MapType'], () => {
    // 地图类型切换
    const type = new this.AMap.MapType({
        defaultType: 0, // 使用2D地图 1为卫星底图
    });
    this.map.addControl(type); // 将图层切换插件绑到地图对象中
});
~~~



