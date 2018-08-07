# 小程序 Demo 演示

该 Demo 主要用于熟悉原生小程序的原生开发模式，安装微信开发者工具导入代码目录即可预览小程序，效果如下图所示

![](http://ochyazsr6.bkt.clouddn.com/dd50616656113a9b3ca324af2fb4fb36.jpg)


## 代码结构

一个原生的小程序包含一个描述整体程序的 app 和多个描述各自页面的 page。

其中主体部分由三个文件组成，必须放在项目的根目录，而一个小程序页面由四个文件组成，如下所示：

```
.
├── README.md
├── app.js      // 主体逻辑
├── app.json    // 公共配置
├── app.wxss    // 公共样式表
├── pages       // 小程序页面
│   ├── index   // 页面一
│   │   ├── index.js     // 页面逻辑
│   │   ├── index.json   // 页面配置
│   │   ├── index.wxml   // 页面结构
│   │   └── index.wxss   // 页面样式表
│   └── logs    // 页面二
│       ├── logs.js
│       ├── logs.json
│       ├── logs.wxml
│       └── logs.wxss
├── project.config.json  // 开发工具配置
└── utils       // 工具类
    └── util.js
```


## 小程序配置

小程序配置都位于代码中的 json 文件中，其中 app.json 中为全局配置，各个 page 中的 json 是页面配置。

- 全局配置

以添加 Tab 为例演示全局配置

```json
"tabBar":{
    "list":[{
      "pagePath": "pages/index/index",
      "text": "index"
    },{
      "pagePath": "pages/logs/logs",
      "text": "logs"
    }]
  }
```

tabBar 还可以添加 position iconPath 等属性，注意 position 为 top 时将隐藏 icon


- 页面配置

每个页面的 `.json` 中也可以对当前页面的表现进行配置，但是只能设置部分 window 配置项的内容，可以演示配置 window 项


## 逻辑层

小程序基于 JavaScript 进行逻辑层开发，开发者的所有代码最终都会被打包成一个 js 文件，而小程序则为开发者提供了 JavaScript 的运行环境。

但是需要注意的是小程序的运行环境和浏览器有所区别，没有浏览器中的 window、 document 等全局变量，但是新增了独有的一些变量和方法。


### 注册 APP

使用 App() 函数可以用来注册一个小程序，在 App() 中可以指定小程序的生命周期函数，例如 onLaunch、onShow、onError 等。 另外 getApp() 是一个全局函数，可以用来随处获取小程序实例。


### 注册 Page

Page() 函数可以用来注册一个页面，在函数中可指定页面的初始数据（data）、生命周期函数（onShow、onReady etc.）、页面事件处理函数（onPullDownRefresh、onTabItemTap etc.）以及 组件事件处理函数。

所谓组件事件处理，就是定义在组件中绑定的事件处理函数，例如本例中 bindViewTap 事件处理函数。

另外值得注意的还有 setData 函数，该函数用于将数据从逻辑层发送到视图层，同时改变 this.data 中的值，如果直接设置 this.data 视图不会随之改变。

## 视图层

框架的视图层由 WXML 与 WXSS 编写，由组件来进行展示。其中 WXML(WeiXin Markup language) 用于描述页面的结构，WXSS(WeiXin Style Sheet) 用于描述页面的样式。

**注意：**  `<block/>` 并不是一个组件，它仅仅是一个包装元素，不会在页面中做任何渲染，只接受控制属性。

### 模板

WXML 提供模板（template），可以在模板中定义代码片段，然后在不同的地方调用。定义模板时使用 name 属性，作为模板的名字。然后在 `<template/>` 内定义代码片段；使用模板时使用 is 属性，声明需要的使用的模板，然后将模板所需要的 data 传入。

### 事件

事件是视图层到逻辑层的通讯方式，可以将用户的行为反馈到逻辑层进行处理。在组件中使用 `bindTap`（冒泡事件） or `catchTap`（非冒泡事件）绑定一个事件处理函数，然后在相应的 Page 定义中写上相应的事件处理函数，参数是 event。

> 事件绑定的写法同组件的属性，以 key、value 的形式。key 以 bind 或 catch 开头，然后跟上事件的类型，如 bindtap、catchtouchstart。自基础库版本 1.5.0 起，bind 和 catch 后可以紧跟一个冒号，其含义不变，如 bind:tap、、catch:touchstart。


## 总结

小程序开发框架提供了自己的视图层描述语言 WXML 和 WXSS，以及基于 JavaScript 的逻辑层框架，并在视图层与逻辑层间提供了数据传输和事件系统，能够让开发者能够专注于数据与逻辑。通过上面的介绍，可以基本了解一个原生小程序的代码结构及其实现逻辑。

但是如果要从零开发一个小程序，对于当前大多数习惯于 mvvm 架构模式（Angular、React、Vue）的开发者而言，这样的开发框架仍然有一定的学习成本，好在微信官方推出了一个类似于 vue.js 的支持组件化的小程序开发框架 WePY，接下来会以助理小咚为例详细介绍。 


## 参考文档

- [微信开发者工具](https://developers.weixin.qq.com/miniprogram/dev/devtools/devtools.html)
- [小程序开发框架](https://developers.weixin.qq.com/miniprogram/dev/framework/MINA.html)
- [微信公众平台](https://mp.weixin.qq.com/?url=%2Fwxopen%2Fcategory%3Faction%3Dget%26token%3D1820933982%26lang%3Dzh_CN)


