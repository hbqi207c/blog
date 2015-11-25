title: Sublime-Text3
date: 2015-11-15 11:16:09
tags: sublimetext
categories: 教程
comments: true
---
> 不知道哪一天在网上看到有人评测Sublime-text，说绝对是开发神器，不是nodepad++等所比拟的（可能有人会说这个有待商议），所以我就去试了一下（本来只是简单的编码，还是菜鸟=.=也谈不上有多少深入），期间也已经用了很长一段时间了也没打算写什么，最近正好想用markdown写点东西，乘此机会写个这个权当熟悉一下markdown的语法。

<!--more-->

## 安装Sublime-Text3
官网有Sublime-Text3和Sublime-Text2，选择ST3下载，[Sublime-Text3](http://c758482.r82.cf2.rackcdn.com/Sublime%20Text%20Build%203083.zip)

安装好Sublime-Text3后还需要安装Package-Control一个必备的包管理，以后用来安装其他插件，安装步骤:
 
 - 1.打开ST，点击菜单View->Show Console
在底部的命令行下输入如下代码并等待安装完成
```bash
import urllib.request,os,hashlib; h = 'eb2297e1a458f27d836c04bb0cbaf282' + 'd0e7a3098092775ccb37ca9d6b2e4b7d'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```
 - 2.安装完成后重启ST3，点开菜单Preference，可以看到package settings和package control则说明安装成功

## 安装插件
经过上面的步骤我们已经成功安装了Package Control，接下来安装插件，快捷键`ctrl+shift+p`打开Package Control,在输入框里输入install，然后会有提示并选择Install Package，等待···然后又弹出一个输入框让你输入插件的名字，输入后回车等待一会儿即可完成插件安装

#### 常用插件
 - Alignment 美化对其"=","`","；"这些符号
 - BracketHighlight 	代码块括号高亮工具，可以自定义括号颜色
 - DocBlockr 在函数上一行输入/**然后回车，神奇的事情发生了，jsdoc就生成了
 - Emmet 以前叫zencoding，快速编写html的一个插件
 - HTML-CSS-JS Prettify html、css、js文件一键优化，但貌似只会优化缩进
 - AngularJS 编写Angular时给出智能提示
 - JQuery JQueryAPI的智能提示
 - SublimeLinter-jshint 配合使用，支持js语法规则校验，每个js编写者必备
 - Markdown Preview 写markdown的好搭档，用来显示预览md格式文件的效果
 - Sidebarenhancements 侧边工具栏增加功能

## 使用教程
如果你想深入试用，并提高效率那么一些快捷键和配置是必不可少的
#### 通用快捷键
* `ctrl_shift+p`
	> 打开Package Control，上面已经介绍过了。这里还有个技巧，此技巧在下面的各种地方都能用的上，就是ST支持模糊匹配。比如，你想找Install Package，你在 Package Control 的输入框中install，可以自动匹配到Install Package，也可以简单的输入ip，也能匹配到它，这种模糊匹配的功能很方便
* `Ctrl+P`
	> 根据文件名打开文件。比如你想打开login/func/funtion.php，你只要在输入框中输入login/func/funtion.php即可，也可以用模糊匹配，如login/function等，模糊匹配还是自己去体验吧
* `ctrl+r`
	> 查找对应的函数和方法，大家注意到了输入框中自动会有一个“@”符号，除此之后还有其他一些匹配符号，如“：”是定位到行
* `ctrl+d`
	> 多处同步编辑，如需要把user换成member只需要双击user然后`ctrl+d`再修改，神奇的事情发生了，where amazing happens！
* `ctrl+f`&`ctrl+shift+f`
	> `ctrl+f`查找就不多说了，`ctrl+shift+f`是全项目查找

待更新···