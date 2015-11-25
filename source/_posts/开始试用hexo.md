title: 开始试用hexo
date: 2015-11-08 18:47:52
tags: hexo
categories: 教程
comments: true
---
引用官网对[hexo](https://hexo.io/zh-cn/)的介绍：快速、简洁且高效的博客框架:
> 超快速度
Node.js所带来的超快生成速度，让上百个页面在几秒内瞬间完成渲染
> 一键部署
只需一条指令即可部署到 GitHub Pages, Heroku 或其他网站
> 支持 Markdown
Hexo 支持 GitHub Flavored Markdown的所有功能，甚至可以整合 Octopress 的大多数插件
> 丰富的插件
Hexo 拥有强大的插件系统，安装插件可以让 Hexo 支持 Jade, CoffeeScript

<!--more-->

## 安装hexo
### 1.安装前提
安装hexo前查看[nodejs](https://nodejs.org/dist/v4.2.1/node-v4.2.1-x86.msi)、[git](http://github-for-windows.en.softonic.com/download)是否安装完成,如果还未安装，下载选择默认安装即可

### 2.安装hexo
安装前我们可以先查看nodejs、git是否安装成功:打开cmd，运行以下命令，如果显示版本号则说明安装正确
```bash
node -v
```
```bash
git --version
```
#### npm安装hexo
```bash
npm install -g hexo-cli #三种方式均可
npm install hexo --no-optional
npm install hexo
```
#### 建站
安装hexo完成后执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件
```bash
hexo init <folder>
cd <folder>
npm install
```

#### 生成静态文件
每次修改文件后都需要生成静态文件
```bash
hexo g
```

#### 启动本地服务
```bash
hexo s
```

至此，hexo本地安装已经完成，打开[http://localhost:4000/](http://localhost:4000/)查看效果

### 3.git部署hexo
#### 修改_config.yml
打开_config.yml，找到deloy
```
deploy: 
  type: git
  repository: https://github.com/yourname/yourname.github.io.git  
  branch: master
  #经测试，“：”后加空格执行hexo d会报错，取消后没问题，不知道什么原因
```

#### 提交web目录到git
假设你已经熟悉git基础命令，打开git bash,cd到hexo安装目录下的public目录(github事先已经建好仓库,仓库名为yourname.github.io，yourname是你的git帐号名)
```bash
git init
git add .
git commit -m 'first commit hexo'
git remote add origin https://github.com/yourname/yourname.github.io.git         #可能要输入你git的用户名和帐号等一些简单步骤
```
结束，至此hexo已经托管到git，以后每次在本地编辑文件后只需要执行以下命令就可以把本地修改提交到git
```bash
hexo g        #生成静态文件
hexo d        #部署
```