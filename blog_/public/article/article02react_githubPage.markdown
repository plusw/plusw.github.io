### [部署react+vite网页项目到Github Page](https://plusw.github.io/blog/#article/article02react_githubPage)
*2023, 12.22*  
    Github page提供免费的静态站点，如果想部署自己的静态博客，没有用到数据库的话，github page是一个不错的选择。我最近将本地的react+vite项目部署到github page，过程有遇一些坑，今天把它分享出来。  
##### 简介
如何将react+vite项目提交到github page，请看[这个视频](https://www.youtube.com/watch?v=XhoWXhyuW_I),很详细
##### Issues
1.出现静态资源找不到的问题
    我的blog地址为 https://yourName.github.io/blog/, 其中blog是我的仓库名，我遇到过fetch /blog/public/img/header.jpg ，总是出现资源找不到，后来用绝对路径 https://yourName.github.io/blog/public/img/header.jpg还是找不到。
    最后我新建了一个 myName.github.io仓库，把资源放在这个仓库下就可以找到，（myName是用户名），
    原来只有 https://yourName.github.io/ 下可以被公共访问
 