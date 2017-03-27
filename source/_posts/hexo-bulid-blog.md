---
title: Hexo 搭建 GitHub 博客
---

自己搭建的时候，也遇到过不少坑，网上查过资料有点乱，有的把 git 安装介绍的很详细，但其实有些多余的，所以自己整理回报一下，这个博客的第一次就奉献给大家了。git npm 等等这些基本，就不详细介绍。唠叨完了，大概需要这么几个体位：

一、GitHub 准备
二、Hexo 本地启动
三、Hexo 配置&生产&上传

我看了网上好多资料，Hexo 问题居多，
Hexo 无法启动？插件安装不全
Hexo 上传失败？配置文件格式不对


All right, let's start with it. Try and do.

## 一、GitHub 准备
GitHub 创建一个 xxx.github.io 的 repository，xxx 为你 GitHub 的帐户名。
Blog 根本上是用的是 GitHub Pages 功能，所以记得在 repository 的设置中打开，一直点下一步，直到你打开 `https://xxx.github.io` ，你就成功了！

然后 clone 到本地
``` bash
git clone git@github.com:xxx/xxx.github.io.git
```

## 二、Hexo 本地启动

``` bash
cd xxx.github.io
npm install hexo-cli -g   #安装 hexo
hexo init   #初始化 hexo
npm install #安装 hexo 其他插件
hexo server #启动 hexo 本地浏览服务
```

假如你遇到问题，可能是不同版本的插件有区别，所以有的需要自己手动安装，下面是一个基本的本地环境插件参考。（ps:现在工具插件化，会把有些功能独立出去，因为定位发生改变，所以默认安装插件也会发生改变）

``` bash
{
  "name": "hexo-site",
  "version": "0.0.0",
  "private": true,
  "hexo": {
    "version": "3.2.2"
  },
  "dependencies": {
    "hexo": "^3.2.0",
    "hexo-deployer-git": "^0.2.0",   #上传 GitHub 插件
    "hexo-generator-archive": "^0.1.4",
    "hexo-generator-category": "^0.1.3",
    "hexo-generator-index": "^0.2.0",
    "hexo-generator-tag": "^0.2.0",
    "hexo-renderer-ejs": "^0.2.0",
    "hexo-renderer-marked": "^0.2.10",
    "hexo-renderer-stylus": "^0.3.1",
    "hexo-server": "^0.2.0"   #本地浏览服务
  }
}
```


## 三、Hexo 配置&生产&上传

配置 GitHub 仓库地址，配置文件的空格都不能错，否则会报错！
``` bash
deploy:
  type: git
  message: "xxx"
  repo: git@github.com:xxx/xxx.github.io.git,master
```
确保电脑已经 ssh 绑定 GitHub，然后

``` bash
hexo clean
hexo generate
hexo deploy
```
上传成功，就大功告成！
尽情的浏览自己的个人博客吧 `https://xxx.github.io`


## 常用命令

``` bash
hexo new "postName"   #新建文章
hexo new page "pageName"   #新建页面
hexo generate   #生成静态页面至 public 目录
hexo server   #开启预览访问端口（默认端口4000）
hexo deploy   #将 .deploy 目录部署到 GitHub
hexo help   #查看帮助
hexo version  #查看 Hexo 的版本
```