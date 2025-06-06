---
title: 网站robots.txt怎么写
layout: post
category: article
---
今天给自己的网站加了一个robots.txt，在网上收集整理了一些资料，给自己网站也加上了robots.txt ！ 顺便给大家分享一下！

## 一、robots.txt是什么？
　　robots.txt是一个纯文本文件，在这个文件中网站管理者可以声明该网站中不想被搜索引擎访问的部分，或者指定搜索引擎只收录指定的内容。
　　当一个搜索引擎（又称搜索机器人或蜘蛛程序访问一个站点时，它会首先检查该站点根目录下是否存在robots.txt，如果存在，搜索机器人就会按照该文件中的内容来确定访问的范围；如果该文件不存在，那么搜索机器人就沿着链接抓取。

## 二、robots.txt的作用

1、引导搜索引擎蜘蛛抓取指定栏目或内容；
2、网站改版或者URL重写优化时候屏蔽对搜索引擎不友好的链接；
3、屏蔽死链接、404错误页面；
4、屏蔽无内容、无价值页面；
5、屏蔽重复页面，如评论页、搜索结果页；
6、屏蔽任何不想被收录的页面；
7、引导蜘蛛抓取网站地图；
## 三、Robots的语法（三个语法和两个通配符）

三个语法如下：
1、User-agent:（定义搜索引擎）
示例：
 User-agent: *（定义所有搜索引擎）
 User-agent: Googlebot （定义谷歌，只允许谷歌蜘蛛爬取）
 User-agent: Baiduspider （定义百度，只允许百度蜘蛛爬取）
 不同的搜索引擎的搜索机器人有不同的名称，谷歌:Googlebot、百度:Baiduspider、MSN:MSNbot、Yahoo:Slurp。
2、Disallow:（用来定义禁止蜘蛛爬取的页面或目录）
 示例：
```text
 Disallow: /（禁止蜘蛛爬取网站的所有目录 "/" 表示根目录下）
 Disallow: /admin （禁止蜘蛛爬取admin目录）
 Disallow: /abc.html （禁止蜘蛛爬去abc.html页面）
 Disallow: /help.html （禁止蜘蛛爬去help.html页面）
3、Allow:（用来定义允许蜘蛛爬取的页面或子目录）
```
 示例：
```text
 Allow: /admin/test/（允许蜘蛛爬取admin下的test目录）
 Allow: /admin/abc.html（允许蜘蛛爬去admin目录中的abc.html页面）
```
两个通配符如下：
4、匹配符 “$”
 $ 通配符：匹配URL结尾的字符
5、通配符 “*”
　　　　* 通配符：匹配0个或多个任意字符

## 四、robots.txt 综合示例

1、禁止搜索引擎抓取特定目录
 在这个例子中，该网站有三个目录对搜索引擎的访问做了限制，即搜索引擎不会访问这三个目录。
```text
 User-agent: *
 Disallow: /admin/
 Disallow: /tmp/
 Disallow: /abc/
```
2、禁止admin目录，但允许抓取admin目录下的seo子目录
```text
 User-agent: *
 Allow: /admin/seo/
 Disallow: /admin/
```
3、禁止抓取/abc/目录下的所有以".htm”为后缀的URL（包含子目录）
```text
 User-agent: * 
 Disallow: /abc/*.htm$
```
4、禁止抓取网站中所有的动态页面
```text
 User-agent: *
 Disallow: /*?*
 ```
屏蔽所有带“?”的文件，这样就屏蔽所有的动态路径。
5、禁止百度蜘蛛抓取网站所有的图片：
```text
 User-agent: Baiduspider
 Disallow: /*.jpg$　　Disallow: /*.jpeg$
 Disallow: /*.gif$　　Disallow: /*.png$
 Disallow: /*.bmp$
```
6、要在阻止网站页面被抓取的同时仍然在这些页面上显示 AdSense 广告
```text
 User-agent: *
 Disallow: /folder1/
 User-agent: Mediapartners-Google
 Allow: /folder1/
```
　　请禁止除 Mediapartners-Google 以外的所有漫游器。 这样可使页面不出现在搜索结果中，同时又能让 Mediapartners-Google 漫游器分析页面，从而确定要展示的广告。 Mediapartners-Google 漫游器并不与其他 Google User-agent 共享网页。

## 五、注意事项

1、robots.txt 文件必须放在网站的根目录，不可以放在子目录。
 以一毛博客网站为例：比如通过 https://GXC.LA/robots.txt 你就可以访问 GXC.LA的robots.txt文件了。
2、robots.txt 文件名命名必须小写，记得在robot面加“s”。
3、User-agent、Allow、Disallow的 “:” 后面有一个字符的空格。
4、路径后面加斜杠“**/**” 和不加斜杠的是有区别的
 Disallow: /help
禁止蜘蛛访问 /help.html、/helpabc.html、/help/index.html
 Disallow: /help/　
 禁止蜘蛛访问 /help/index.html。 但允许访问 /help.html、/helpabc.html
5、Disallow与Allow行的顺序是有意义的：
 举例说明：
 允许蜘蛛访问 /admin/ 目录下的user文件夹
 User-agent: *
 Allow: /admin/user/
 Disallow: /admin/
 如果Allow 和 Disallow 的顺序调换一下：
 User-agent: * 
 Disallow: /admin/
 Allow: /admin/user/
蜘蛛就无法访问到 /admin/ 目录下的 user 文件夹，因为第一个 Disallow: /admin/ 已匹配成功。
## 六、关于Robots Meta

 Robots.txt文件主要是限制整个站点或者目录的搜索引擎访问情况，而Robots Meta标签则主要是针对一个个具体的页面。和其他的META标签（如使用的语言、页面的描述、关键词等）一样，Robots Meta标签也是放在页面中，专门用来告诉搜索引擎ROBOTS如何抓取该页的内容。
 Robots Meta 标签中没有大小写之分，name="Robots" 表示所有的搜索引擎，可以针对某个具体搜索引擎（如google）写为 name="Googlebot"， content部分有四个指令选项：index、noindex、follow、nofollow，指令间以 “,” 分隔。
 Index 指令告诉搜索机器人抓取该页面；
 NoIndex命令：告诉搜索引擎不允许抓取这个页面
 Follow 指令表示搜索机器人可以沿着该页面上的链接继续抓取下去；
 NoFollow命令：告诉搜索引擎不允许从此页找到链接、拒绝其继续访问。
 Robots Meta 标签的缺省值是Index和Follow；
 根据以上的命令，我们就有了一下的四种组合：
 可以抓取本页，而且可以顺着本页继续索引别的链接=
 不许抓取本页，但是可以顺着本页抓取索引别的链接
 可以抓取本页，但是不许顺着本页抓取索引别的链接
 不许抓取本页，也不许顺着本页抓取索引别的链接。
## 七、关于 rel="nofollow"

　　将"nofollow"放在超链接中，告诉搜索引擎不要抓取特定的链接。
　　如某博客上有垃圾评论：灌水
就是这些注意事项了，大家去试试robots.txt吧！
