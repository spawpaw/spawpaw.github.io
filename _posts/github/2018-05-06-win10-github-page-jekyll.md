---
layout: post
title:  "Win10 管理gihub-page项目"
date:   2018-05-06 12:46:00 +0800
categories: github
tags: 
---

由于在GitHub上直接编辑文章非常麻烦，所以想办法在win10上搭建实时预览的环境（日常需要经常用win10，所以不用linux）

有两种方法，一种是直接在IDE里预览，一种是实时编译站点，然后再浏览器中预览

## 使用vscode+markdown预览插件
安装vscode，并在vscode中安装markdown相关的插件，即可实时预览，缺点是布局可能和push上去之后的不一样


## 使用jekyll在本机编译站点
1. WSL: 安装win10 Linux子系统
2. jekyll: 在linux子系统上安装jekyll(`apt-get install jekyll`)，在`xxx.github.io`目录下运行`jekyll serve`
3. IIS: 在win10上打开IIS，然后新建一个http站点，将根目录指向项目根目录的`_site`文件夹
4. 在浏览器中直接访问IIS上搭建的站点

这样就可以获得和push后一样的浏览效果

(windows装jekyll的环境太麻烦，所以迂回以下反而更方便些)