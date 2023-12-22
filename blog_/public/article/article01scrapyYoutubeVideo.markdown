### [使用selenium+youget批量下载Youtube视频](https://plusw.github.io/blog/#article/article01scrapyYoutubeVideo)
*2023, 12.22*  
    经常在youtube上听歌，在其他音乐平台很多需要版权，于是想把youtube上，我的播放列表里的歌曲全部下载。最近学习了爬虫，写了这个项目，用selenium爬取歌曲信息，使用you-get下载到本地。
##### 简介
1.项目使用python,首先安装chrome driver,安装对应版本的chrome。
2.使用selenium控制chrome打开网页, 使用xpath定位歌曲元素
3.然后将歌曲信息字符串储存在本地csv文件。
4.为了防止下载已经下载过的歌曲，在下载前对比本地mp3文件夹下的mp3，将已下载的做标记。 
5.读取csv文件，使用you-get下载未标记的歌曲
6.下载后将mp4转为mp3。
##### Issues
you-get偶尔失败，原因:you-get使用多次会被Youtube检测出来，最好使用ip代理
##### Detail
###### 初始化selenium
```python
options = Options()
options.binary_location = "W:/chrome/chrome-win64/chrome.exe"  # 指定chrome路径
path = Service(r'W:\chromeDriver\chromedriver-win64\chromedriver.exe')# 指定driver路径
driver = webdriver.Chrome(service=path, options=options)
website = "https://www.youtube.com/playlist?list=PLzq2u2o3_5PIETb3Lzhc83QL"
driver.get(website)
```
###### you-get下载
```python
import you_get
sys.argv = ['you-get', '-o', outputPath, inputLink, "-O", outputName,"--debug"]
you_get.main()
```
###### 完整代码
```python
import time
import pandas as pd
from selenium import webdriver
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.chrome.service import Service
# from pytube import YouTube
import os
import re
import you_get
import sys
from moviepy.editor import *



def main():
    scrapy()
    compare_music_library_and_csv_file()
    read_csv_and_download()
    # rename_onlyAudio_mp4_to_mp3()

def mp4ToMp3(inputMp4_name,outputMp3_name):
    # Load the mp4 file
    video = VideoFileClip(inputMp4_name)
    # Extract audio from video
    video.audio.write_audiofile(outputMp3_name)
def rename_onlyAudio_mp4_to_mp3():
    all_flies = os.listdir('./download/mp4')
    for file in all_flies:
        if (file[-4:] == ".mp4" or file[-4:] == ".mp3"):
            try:
                os.rename("./download/mp4/" + file, f"./download/mp3/{file[:-4] + '.mp4'}")  # rename and move
                mp4ToMp3(f"./download/mp3/{file[:-4] + '.mp4'}",f"./download/mp3/{file[:-4] + '.mp3'}") #mp4 to mp3
                os.remove(f"./download/mp3/{file[:-4] + '.mp4'}") #remove mp4
            except Exception as e:
                print("something wrong when rename:",e)
        else:
            os.remove("./download/mp4/" + file)


def download(inputLink, outputName, outputPath):
    # sys.argv = ['you-get', '-o', outputPath, "--itag=160", inputLink, "-O", outputName]
    sys.argv = ['you-get', '-o', outputPath, inputLink, "-O", outputName,"--debug"]
    you_get.main()


def read_csv_and_download():
    df = pd.read_csv('downloadMusic.csv')
    for i in range(len(df.index)):
        judge = str(df.loc[i, 'download'])
        if (judge == "True"):
            print(str(df.loc[i, 'video_name']) + ".mp3 already exist")
        else:
            print("downloading..." + str(df.loc[i, 'video_name']))
            video_name = df.loc[i, 'video_name']
            video_link = df.loc[i, 'video_link']
            download(video_link, video_name, "./download/mp4")
            rename_onlyAudio_mp4_to_mp3()


def get_all_mp3_file_name_in_music_library():
    mp3_file = []
    all_flies = os.listdir('./download/mp3')
    for file in all_flies:
        if (file[-4:] == ".mp3"):
            mp3_file.append(file)
    return mp3_file


def compare_music_library_and_csv_file():
    file_in_music_library = get_all_mp3_file_name_in_music_library()
    df = pd.read_csv('downloadMusic.csv')
    for i in range(len(df.index)):
        file_in_csv = str(df.loc[i, 'video_name']) + ".mp3"
        if file_in_csv in file_in_music_library:
            df.loc[i, 'download'] = "true"
            df.to_csv("downloadMusic.csv")


def getRegularString(text):
    import re
    result = re.findall('[\u4e00-\u9fa5a-zA-Z0-9]+', text, re.S)  # 只要字符串中的中文，字母，数字
    result = "".join(result)
    return result


video_names = []
video_links = []


def scrapy():
    options = Options()
    options.binary_location = "W:/chrome/chrome-win64/chrome.exe"  # 指定chrome路径
    path = Service(r'W:\chromeDriver\chromedriver-win64\chromedriver.exe')
    driver = webdriver.Chrome(service=path, options=options)

    website = "https://www.youtube.com/playlist?list=PLzq2uGSJ2o3_5PIETb3LzDFyZ75hc83QL"
    driver.get(website)

    time.sleep(3)

    ytd_playlist_video_list_renderer = driver.find_element("xpath",
                                                           "//ytd-playlist-video-list-renderer[contains(@class, 'style-scope ytd-item-section-renderer' )]")

    all_video_title_a = ytd_playlist_video_list_renderer.find_elements("xpath", "//a[@id='video-title']")
    for video_title_a in all_video_title_a:
        video_names.append(getRegularString(video_title_a.text))
        video_link = video_title_a.get_attribute('href')
        video_link = "https://www.youtube.com/" + re.search(r'https://www.youtube.com/(.*?)&', video_link).group(1)
        video_links.append(video_link)
    df = pd.DataFrame({'video_name': video_names, 'video_link': video_links, 'download': ""})
    df.to_csv("downloadMusic.csv")
    time.sleep(1)


main()

```


