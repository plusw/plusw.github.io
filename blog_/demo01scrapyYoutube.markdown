### [使用selenium+youget批量下载Youtube视频](https://example.com)
*Posted by plusw on December 17, 2023*  
    经常在youtube上听歌，于是想把youtube上，我的播放列表里的歌曲全部下载。
用到了selenium爬取歌曲信息，使用you-get下载到本地。项目使用python,首先启动
selenium, 定位歌曲，将爬取的所有需要下载的歌曲信息储存在本地csv文件。然后对
比mp3文件夹，将已下载的做标记，防止重复下载, 然后读取csv文件，使用you-get下
载，下载后将mp4转为mp3。
#### 正文


