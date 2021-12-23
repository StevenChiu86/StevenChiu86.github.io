---
title: Hexo 基本設定(安裝與共用)
date: 2021-05-29 00:47:11
tags: Insatll and Setting
categories: Blog Setting
---

# Hexo 基本設定(安裝與共用)
記錄下如何自己架設hexo blog 
## 建立Blog

### 創建githubpage
1.  Github上建立名稱為 StevenChiu86.github.io的public repository 

###  下載hexo相關安裝包
1. 安裝node.js, git
2. 安裝hexo相關套件
    ```
    npm install -g hexo-cli
    hexo init name  //初始化新的 Hexo，會在當前路徑建立一個叫 name 的資料夾，資料夾名稱可以隨意取，例如「myblog」，那麼指令就是 hexo init myblog
    cd name  //進入您剛剛建立的 name 資料夾當中，cd 是 change directory 的意思
    npm install  //安裝 Hexo
    npm install hexo-deployer-git --save  //安裝 git 部署套件
    ```
3. 設定_config.yaml檔案
   打開 _config.yml 後，修改第 6~12 行資訊，輸入完記得按下 Ctrl+S 存檔(# 為註解)：
   ```
    title: Steven's Blog
    subtitle: '努力努力再努力_YOLO'
    description: '這是Steven的blog, 分享些科技、生活、音樂等小記事, 歡迎大家來'
    keywords: Stevenblog
    author: Steven
    language: zh-TW
    timezone: ''
   ```
4. 接著第 16 行的地方，url 請換成自己網站的連結 https://username.github.io/ ，username是自己的 GitHub 帳號。
5. 設定部署至 GitHub 的資訊
* 一樣在_config檔案裡面
    ```
    deploy:
    type: git
    repository: https://github.com/StevenChiu86/StevenChiu86.github.io.git
    branch: master
    ```
6. 佈署至github
    ```
    hexo cl  //清除之前建立的靜態檔案，也可以輸入 hexo clean
    hexo g  //建立靜態檔案，也可以輸入 hexo generate
    hexo d  //部署至 Github Pages，也可以輸入 hexo deploy
    ```
7.  在本地端查看blog,打 `hexo s` 就能透過瀏覽器打localhost:4000 查看, 透過重新整理可以查看當前blog撰寫的樣子

### 上網選第三方主題
1. 首先進入theme目錄 `cd /themes`
2. git clone [第三方主題網址]
3. 修改_config檔案裡面的 `theme:[第三方主題名稱]`
4. 刪除第三方主題的.git檔案
    * 從別人的github下載主題後,經過自己的更改後要pull到github上,需要先到themes/[主題名稱]下的.git刪除(因為在有.git的資料夾下, 不能包含.git的資料夾),才能成功pull themes到github上

## 不同電腦下同步修改hexo部落格
[[教學] 使用 GitHub Pages + Hexo 來架設個人部落格](https://ed521.github.io/2019/07/hexo-install/)
[如何在不同电脑上同时写hexo博客？](https://chown-jane-y.github.io/2017/03/15/%E5%A6%82%E4%BD%95%E5%9C%A8%E4%B8%8D%E5%90%8C%E7%94%B5%E8%84%91%E4%B8%8A%E5%90%8C%E6%97%B6%E5%86%99hexo%E5%8D%9A%E5%AE%A2%EF%BC%9F/)
### 原本電腦操作
1. 在github下先刪除master裡面的資料, 然後創建一個叫hexo的branch(用於更新最新blog), 並把它變成default
2. 在本地也創建hexo branch `git branch hexo`
3. 然後先把所有修改加入 `git add .` (要先把第三方主題的.git刪掉(在themes/[主題名稱]下))
4. 提交`git commit -m "第一次push_同步給其他電腦使用"`
5. git push origin hexo

### 新的電腦操作
1. `git clone "https://github.com/StevenChiu86/StevenChiu86.github.io"`
2. 下載相關hexo套件跟依賴
    ```
    npm install hexo
    npm install
    npm install hexo-deployer-git –save
    ```
3. 接下來就可以在新電腦上編輯bolg拉!!!
4. 編輯完後, 提交
    ```
    git add .
    git commit -m "你想留的資訊"
    git push origin hexo
    ```
## Blog功能

* 新增文章: `$hexo new post xxx`, 就會在source資料夾下產生xxx.md

## 新增加圖片
[解决Hexo图片无法显示问题](https://blog.csdn.net/weixin_30734435/article/details/98497054)
1. 根目錄下配置文件_config.yml 中有 post_asset_folder:false 改為 true
    * 這樣 hexo n "文章名稱", 就會自動在 source/post 下新增相同名稱資料夾(需要上傳的圖片放入)
2. 安裝 git bash 套件 `npm install https://github.com/7ym0n/hexo-asset-image --save`
3. 文章內插入圖片方式：{% asset_img xxx.jpg %}
