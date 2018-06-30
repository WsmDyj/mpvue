
### mpvue快速搭建美团外卖（第三方）微信小程序
测试推动2018/6/16 20:22
### 项目使用的技术栈
* 数据请求: [flyio.js](https://github.com/wendux/fly)- 同时支持浏览器、小程序、Node、Weex的基于Promise的跨平台http请求库。可以让您在多个端上尽可能大限度的实现代码复用
* css预编译器: [stylus](https://www.zhangxinxu.com/jq/stylus/)-基于Node.js的CSS的预处理框架
* 数据来源:[EasyMock](https://www.easy-mock.com/mock/5aded45053796b38dd26e970/sell#!method=get)-为测试提供模拟数据
* 整体框架: [mpvue](https://github.com/Meituan-Dianping/mpvue)
* 地图:[腾讯地图api](https://developers.weixin.qq.com/miniprogram/dev/api/)

### 下载启动步骤
* 1、git clone [https://github.com/WsmDyj/mpvue.git](https://github.com/WsmDyj/mpvue.git)
* 2、安装启动
```
# install dependencies
npm install
# serve with hot reload at localhost:8080
npm run dev
# build for production with minification
npm run build
# build for production and view the bundle analyzer report
npm run build --report
```

* 3、小程序开发工具指向下面的dist目录
## 效果图 一起点个外卖吧
![index](https://user-gold-cdn.xitu.io/2018/6/25/164347a3d901b552?w=351&h=628&f=gif&s=2550668)
