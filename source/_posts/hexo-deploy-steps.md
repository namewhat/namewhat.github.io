---
title: hexo异地更新、换电脑更新
date: 2020-02-17 20:16:51
tags: 
- hexo
categories:
- 技术
- hexo
---

### 一、搭建的流程

1. 创建仓库，[http://namewhat.github.io](http://namewhat.github.io)

2. 创建两个分支：master 与 blog

3. master为默认分支，[http://namewhat.github.io](http://namewhat.github.io)指向master分支上的网站文件）

4. 拷贝仓库("-b blog"参数指定克隆分支)
    ``` bash
    git clone -b blog git@github.com:namewhat/namewhat.github.io.git
    ```
          
5. 在本地namewhat.github.io文件夹下通过Git bash依次执行
    ``` bash
    npm install hexo-cli --save
    hexo init
    npm install
    npm install hexo-deployer-git
    ```

6. 依次执行以下git bash指令，推送代码文件到blog分支，方便我们异地或换另一台电脑更新文章
    ``` bash
    git add .
    git commit -m '....'
    git push -u origin HEAD:blog
    ```

7. _config.yml中的deploy参数应为master，我们需要把网站内容推送到默认分支; 
    ``` bash
    deploy:
        type: git
        repo:  https://github.com/namewhat/namewhat.github.io
        branch: master
    ```

8. 部署网站，这条指令会把hexo编译好的静态文件推送到_config.yml中的deploy参数指向的分支，我们这里是“master”分支
    ``` bash
    hexo g -d
    ```
     这样一来，在GitHub上的 http://namewhat.github.io 仓库就有两个分支，一个blog分支用来存放网站的原始文件，一个master分支用来存放生成的静态网页。Get( •̀ ω •́ )y！

### 二、日常创作流程（更新文章、修改样式等等...）

1. 执行以下指令发布网站，推送到默认分支master
    ``` bash
    hexo g -d
    ```

2. 执行以下指令，推送代码到主分支blog
    ``` bash
    git add .
    git commit -m '...'
    git push origin HEAD:blog
    ```

### 三、电脑丢失了？电脑重装了？换台电脑更新？当然是搞得定

1. clone仓库
    ``` bash
    git clone -b blog git@github.com:namewhat/namewhat.github.io.git
    ```

2. 在clone的文件夹路径下，执行以下指令
    ``` bash
    npm install hexo --g
    npm install
    npm install hexo-deployer-git
    ```
    然后就可以愉快的更新文章啦