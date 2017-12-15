title: Hello Hexo
tags:
  - hexo
categories: []
author: mession
date: 2017-11-17 13:19:00
---
Hexo,终于弄好了！
1.安装nodejs
2.安装git
3.新建文件夹进入 
sudo npm install -g hexo （切换淘宝镜像npm config set registry https://registry.npm.taobao.org，查看npm config get registry）
4.hexo init 
5.hexo generate（hexo g）
6.修改 _config.yml 
deploy:
     type: git
     repo: https://github.com/fanyushuai/fanyushuai.github.io.git（到gitgub新建repositories）
     branch: master
7.npm install hexo-deployer-git --save

8.hexo deploy
9.hexo server

注意：每次部署的步骤，可按以下三步来进行。
1.hexo clean
2.hexo generate
3.hexo deploy
一气呵成：hexo clean && hexo g && hexo d



    