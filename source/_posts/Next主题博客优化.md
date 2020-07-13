---
title: hexo Next主题博客优化
date: 2020-05-09 14:03:29
tags:
typora-copy-images-to: upload
---

## 1 在右上角或者左上角实现fork me on github

从文字样式 [GitHub Ribbons](https://github.blog/2008-12-19-github-ribbons/)或[图标样式](http://tholman.com/github-corners/)，选择一个样式模板，并复制文本框中的代码，例如：

![20200509_002](http://q9kx2gcuj.bkt.clouddn.com/20200509_002.png)



其中，href="https://your-url"修改为自己的github用户地址。

打开 themes/next/layout/_layout.swig 文件，把代码复制到<div class="headband"></div>下面

```
<body itemscope itemtype="http://schema.org/WebPage">
  <div class="container{%- if theme.motion.enable %} use-motion{%- endif %}">
    <div class="headband"></div>
	<a href="https://github.com/jialimeng" class="github-corner" aria-label="View source on GitHub"><svg width="80" height="80" viewBox="0 0 250 250" style="fill:#151513; color:#fff; position: absolute; top: 0; border: 0; right: 0;" aria-hidden="true"><path d="M0,0 L115,115 L130,115 L142,142 L250,250 L250,0 Z"></path><path d="M128.3,109.0 C113.8,99.7 119.0,89.6 119.0,89.6 C122.0,82.7 120.5,78.6 120.5,78.6 C119.2,72.0 123.4,76.3 123.4,76.3 C127.3,80.9 125.5,87.3 125.5,87.3 C122.9,97.6 130.6,101.9 134.4,103.2" fill="currentColor" style="transform-origin: 130px 106px;" class="octo-arm"></path><path d="M115.0,115.0 C114.9,115.1 118.7,116.5 119.8,115.4 L133.7,101.6 C136.9,99.2 139.9,98.4 142.2,98.6 C133.8,88.0 127.5,74.4 143.8,58.0 C148.5,53.4 154.0,51.2 159.7,51.0 C160.3,49.4 163.2,43.6 171.4,40.1 C171.4,40.1 176.1,42.5 178.8,56.2 C183.1,58.6 187.2,61.8 190.9,65.4 C194.5,69.0 197.7,73.2 200.1,77.6 C213.8,80.2 216.3,84.9 216.3,84.9 C212.7,93.1 206.9,96.0 205.4,96.6 C205.1,102.4 203.0,107.8 198.3,112.5 C181.9,128.9 168.3,122.5 157.7,114.1 C157.9,116.9 156.7,120.9 152.7,124.9 L141.0,136.5 C139.8,137.7 141.6,141.9 141.8,141.8 Z" fill="currentColor" class="octo-body"></path></svg></a><style>.github-corner:hover .octo-arm{animation:octocat-wave 560ms ease-in-out}@keyframes octocat-wave{0%,100%{transform:rotate(0)}20%,60%{transform:rotate(-25deg)}40%,80%{transform:rotate(10deg)}}@media (max-width:500px){.github-corner:hover .octo-arm{animation:none}.github-corner .octo-arm{animation:octocat-wave 560ms ease-in-out}}</style>
    <header class="header" itemscope itemtype="http://schema.org/WPHeader">
      <div class="header-inner">{% include '_partials/header/index.swig' %}</div>
    </header>
```

保存调试，就会看到效果如下：

![20200509_004](http://q9kx2gcuj.bkt.clouddn.com/20200509_004.png)

## 侧边栏优化

- 个人头像设置
- 社交栏图标设置
- 友情链接设置
- RSS订阅设置

### 头像设置

在主题配置文件搜索avatar字段，配置如下：

```
# Sidebar Avatar
avatar:
  # Replace the default image and set the url here.
  url: /images/avatar.gif
  # If true, the avatar will be dispalyed in circle.
  rounded: false
  # If true, the avatar will be rotated with the cursor.
  rotated: false
```

url是图像存放地址，可以是本地文件路径，也可以是网络地址。本配置使用默认的图片

### 社交栏配置

在主题配置文件中，搜索social，接下来，就看你需要显示什么社交网站，写上网站名+网址

比如原来配置中的网站：

```
# Social Links
# Usage: `Key: permalink || icon`
# Key is the link label showing to end users.
# Value before `||` delimiter is the target permalink, value after `||` delimiter is the name of Font Awesome icon.
social:
  GitHub: https://github.com/yourname || fab fa-github
  #E-Mail: mailto:yourname@gmail.com || fa fa-envelope
  #Weibo: https://weibo.com/yourname || fab fa-weibo
  #Google: https://plus.google.com/yourname || fab fa-google
  #Twitter: https://twitter.com/yourname || fab fa-twitter
  #FB Page: https://www.facebook.com/yourname || fab fa-facebook
  #StackOverflow: https://stackoverflow.com/yourname || fab fa-stack-overflow
  #YouTube: https://youtube.com/yourname || fab fa-youtube
  #Instagram: https://instagram.com/yourname || fab fa-instagram
  #Skype: skype:yourname?call|chat || fab fa-skype
```

### 友情链接配置

打开 主题配置文件,搜索关键字 links：

```
# Blog rolls
links_settings:
  icon: fa fa-link
  title: Links
  # Available values: block | inline
  layout: inline

links:
  Title: http://yoursite.com
  百度: http://www.baidu.com
```

在links字段下，写上名字及其地址。

**备注**：

layout作用：链接站点的排版

block:竖排

inline:横排

### RSS订阅设置

安装网上给的步骤，RSS没有出来，不知道为什么。配置步骤是这样

步骤1：执行安装插件命令

```
$ npm install hexo-generator-feed
```

步骤2：修改站点配置文件，添加如下内容

```
# Extensions
## Plugins: http://hexo.io/plugins/
#RSS订阅
#plugin: 
#- hexo-generator-feed
# feed
# Dependencies: https://github.com/hexojs/hexo-generator-feed
feed:
  type: atom
  path: atom.xml
  limit: 20
  hub:
  content:
  content_limit: 140
  content_limit_delim: ' '
  order_by: -date
  icon: icon.png
  autodiscovery: true
  template:
```

步骤3：最后修改主题配置文件，修改内容如下：

```
follow_me:
  #Twitter: https://twitter.com/username || fab fa-twitter
  #Telegram: https://t.me/channel_name || fab fa-telegram
  #WeChat: /images/wechat_channel.jpg || fab fa-weixin
  RSS: atom.xml || fa fa-rss
```



最后给侧栏的效果如下：

![20200509_005](http://q9kx2gcuj.bkt.clouddn.com/20200509_005.png)



参考：

[Next主题配置文件说明](https://blog.junyu.io/posts/0005-next-theme-settings.html#menu)

[NexT主题的配置和优化指南](https://juejin.im/post/5a71ab9f518825735300ee6c)

[hexo的next主题个性化教程:打造炫酷网站](http://shenzekun.cn/)

[Hexo+Next主题优化](https://zhuanlan.zhihu.com/p/30836436)

[hexo next主题优化，打造个人精致网站](http://eternalzttz.com/hexo-next.html)