### [改变鼠标样式](https://plusw.github.io/blog/#article/article03mouseCurse)
*2023, 12.22*  
    可以改变默认的鼠标样式，比如说把白色箭头改为游戏里的图标。在windows里可以直接在设置里改。在前端网页上可以使用.cur静态图标，也可以使用.ani动态鼠标。

##### **前言**
在windows上改鼠标样式很简单，打开设置，搜索鼠标设定直接改。支持静态和动态鼠标样式。
##### **一.更改网页上的静态鼠标样式.cur**
 css支持更改静态鼠标样式.cur图标，可以在CSS文件里直接加上.
 ```css
 * {
        cursor: url("./path/mouse.cur"), default;
    }
 ```
 上面这行代码表示 用mouse.cur作为鼠标，如果有问题则使用default默认鼠标。
 ##### **二.使用动态鼠标样式.ani文件**
css不支持动态鼠标样式.cur图标，[在网上找到一个库支持.ani](https://www.npmjs.com/package/ani-cursor),感谢国外大神。
[原文点这里](https://github.com/captbaritone/webamp/tree/master/packages/ani-cursor)  
首先安装依赖 ani-cursor  
```bash
npm install ani-cursor
```
下面是完整代码的一个实例:  
index.html
```html
<!DOCTYPE html>
<html>
<head>
    <title>ani-cursor example</title>
    <meta charset="UTF-8" />
    <style>
        #demo {
            width: 300px;
            height: 300px;
            border: 4px dashed black;
            background: pink;
            display: flex;
            justify-content: center;
            align-items: center;
        }
    </style>
</head>
<body>
        <script src="./src/index.js"></script>
</body>
</html>
```
./src/index.js文件
```javascript
import { convertAniBinaryToCSS } from "ani-cursor";
async function applyCursor(selector, aniUrl) {
    const response = await fetch(aniUrl);
    const data = new Uint8Array(await response.arrayBuffer());
    console.log(data)
    const style = document.createElement("style");
    style.innerText = convertAniBinaryToCSS(selector, data);

    document.head.appendChild(style);
}

applyCursor(
    "#demo",
    // "https://archive.org/cors/tucows_169750_Dove_Flying/dove.ani"
    "https://plusw.github.io/blog_/public/source/1.ani"
);
```
项目要启动服务运行，直接双击运行不了。  可以使用Parcel启动服务，也可以用react等等  
这里推荐一个[下载.cur和.ani的网站](https://www.cursors-4u.com/mmorpg/)  