昨天微信小程序（应用号）内测的消息把整个技术社区炸开了锅，
我也忍不住跟了几波，可惜没有内测资格，听闻破解版出来了，
今天早上就着原来的项目资源试开发了一下，总结一下体验.

## 总体体验

1. 开发效率高，6：40左右破解完IDE，7:20左右点做完了首页和导航栏的布局，微信把觉见的布局都做了封装，比传统的前端开发效率高。
2. 前端可以快速上手：熟练的前端可以很快上手，可能只要一小时读文档的时间加一个官方的例子。
3. 开发工具难用，很多目录的操作和IDE常见的格式化代码，html配对等功能暂不支持。
4. 开发限制了很多前端常见的Dom,window操作，开发的灵活度和难度降低。
5. 我没有内测资格，小程序还不能上传体验，只能下载代码本地体验。

> 本文代码放在[github](![image](https://cloud.githubusercontent.com/assets/7630567/18769668/b7ca3a32-8161-11e6-960f-9bcdd0ef66b5.png)
)

**上截图**

![image](https://cloud.githubusercontent.com/assets/7630567/18770171/e0b19bf8-8165-11e6-93d9-6c293c09fce7.png)

![image](https://cloud.githubusercontent.com/assets/7630567/18770220/70afbf14-8166-11e6-987a-c3ff90484ef2.png)

### 相关资源
1. [破解的IDE](https://github.com/gavinkwoe/weapp-ide-crack)
2. [开发资源集合](https://github.com/justjavac/awesome-wechat-weapp) 


## IDE技术栈：NodeWebkit + React

进入的安装目录：微信web开发者工具\package.nw\app   
这个*.nw就能十有八九猜出是NodeWebkit封装的Web应用， 
详看依赖node_modules证实了猜想。
在package.json "main": "app/html/index.html"定义了入口。

### 所有的组件本质是React组件
在入口中可以看到直接引用了React 和React DOM
![image](https://cloud.githubusercontent.com/assets/7630567/18769950/039de2c2-8164-11e6-804a-3aeabdbbef1a.png)

```js
"use strict";
function init() {
    tools.Chrome = chrome;
    var n = require("../dist/lib/react.js"),
        e = require("../dist/lib/react-dom.js"),
        i = require("../dist/common/loadInit/init.js"),
        o = require("../dist/components/ContainController.js"),
        t = require("../dist/common/proxy/startProxy.js"),
        r = require("../dist/actions/windowActions.js"),
        s = require("../dist/actions/webviewActions.js"),
        d = require("../dist/stroes/webviewStores.js"),
        u = require("../dist/common/log/log.js"), c = require("../dist/common/shortCut/shortCut.js"), l = global.appConfig.isDev;
        //...
}
```

看一下组件Dropdown的定义，这不就是我们熟悉的React在ES5中创建组件的方法吗？
```js
"use strict";
var React = require("../../lib/react.js"), Dropdown = React.createClass({
    displayName: "Dropdown", render: function () {
        return React.createElement("div", {className: "dropdown"}, React.createElement("div", {className: "dropdown-item"}, React.createElement("img", {
            src: "https://mmrb.github.io/avatar/jf.jpg",
            alt: "",
            className: "dropdown-item-icon"
        }), React.createElement("div", {className: "dropdown-item-info"}, React.createElement("p", null, "公众号名称啦")), React.createElement("div", {className: "dropdown-item-extra"}, React.createElement("img", {
            src: "https://mmrb.github.io/avatar/jf.jpg",
            alt: "",
            className: "dropdown-item-extra-icon"
        }))), React.createElement("div", {className: "dropdown-item dropdown-item-active"}, React.createElement("img", {
            src: "https://mmrb.github.io/avatar/jf.jpg",
            alt: "",
            className: "dropdown-item-icon"
        }), React.createElement("div", {className: "dropdown-item-info"}, React.createElement("p", null, "公众号名称啦公众号名称啦公众号名称啦"))), React.createElement("div", {className: "dropdown-item"}, React.createElement("img", {
            src: "https://mmrb.github.io/avatar/jf.jpg",
            alt: "",
            className: "dropdown-item-icon"
        }), React.createElement("div", {className: "dropdown-item-info"}, React.createElement("p", null, "公众号名称啦"))), React.createElement("div", {className: "dropdown-item"}, React.createElement("img", {
            src: "https://mmrb.github.io/avatar/jf.jpg",
            alt: "",
            className: "dropdown-item-icon"
        }), React.createElement("div", {className: "dropdown-item-info"}, React.createElement("p", null, "公众号名称啦"))))
    }
});
module.exports = Dropdown;
```

## 微信限制了小程序的包大小

同时微信限制了小程序包的大小，为755kb,对缓存和本地文件应该也有控制，这相对原生应用动不动几十兆上百兆的大小来说，绝对是一个亮点，给网上很多人说装微信小程序同样会占用手机存储的人一个响亮的耳光。

![image](https://cloud.githubusercontent.com/assets/7630567/18769668/b7ca3a32-8161-11e6-960f-9bcdd0ef66b5.png)


## 总结
总的来说，对前端来说绝对是一个好消息，
短期内前端待遇可能上涨，但小程序开发门槛较低（比前端的都低），有一部开发人员是面向工资编程，随着开发人员的流动，长期还是会和其它相关的的技术岗持平。
所以，少年，不要激动，还要是把基础知识打扎实。