---
title: Hexo博客的SEO
date: 2017-04-01 17:03:16
categories:
- Hexo
tags:
- hexo
- next
- seo
keywords:
---

{% asset_img search10.png %}

{% cq %}
好不容易搭建起了第一个属于自己的个人博客站点，然后使用谷歌以及百度搜索自己的博客网站时，突然发现：What?居然搜索不到！！！顿时不禁黯然神伤。。。。。。这个时候，就意味着我们需要对自己的博客，进行SEO！
--TyouSF
{% endcq %}

<!--more-->

{% blockquote 搜索引擎优化 https://zh.wikipedia.org/wiki/%E6%90%9C%E5%B0%8B%E5%BC%95%E6%93%8E%E6%9C%80%E4%BD%B3%E5%8C%96 维基百科 %}
搜索引擎优化（英语：search engine optimization，缩写为SEO），是一种通过了解搜索引擎的运作规则来调整网站，以及提高目的网站在有关搜索引擎内排名的方式。由于不少研究发现，搜索引擎的用户往往只会留意搜索结果最前面的几个条目，所以不少网站都希望通过各种形式来影响搜索引擎的排序，让自己的网站可以有优秀的搜索排名。当中尤以各种依靠广告维生的网站为甚。
{% endblockquote %}

----

# 为什么要SEO

----

当我们拥有自己的博客站点后，我们当然希望我们自己的博客可以在各种的搜索引擎中能够被搜索到。这样，就会有更多的人知道和了解我们，从而让自己小有名气！
可是此时，当我们搭建完毕我们的博客站点后，此时谷歌也好百度也好都是搜索不到的！这是为什么呢？
因为我们的站点**没有被搜索引擎收录**！
那么如何解决想必你也知道方法了：那就是让搜索引擎收录我们的站点。
如何收录呢？接下来就动起手来，让我们的站点被搜索引擎收录吧！

**注**：
* 本文主要以Google搜索为主进行讲解，有关百度的收录，基本与Google操作一致，各位看官可自行动手实现一下，也当是检测自己的掌握情况！
* 本文的优化结果与主题有一定关系，高度适用于使用 NexT 主题进行搭建的 Hexo 博客，其他主题可进行变通
* 为了描述方便，在以下说明中，将位于站点根目录下，主要包含Hexo本身的配置文件称之为：“站点配置文件”，将位于主题目录下的配置文件称之为：“主题配置文件”


----

# 准备工作

----

## 安装 sitemap

为了能够让我们的站点被收录，我们需要为我们的hexo博客安装相关支持的包。这两个包分别为：
- hexo-generator-sitemap 【该包用于支持Google搜索引擎】
- hexo-generator-baidu-sitemap 【该包用于支持百度搜索引擎】

对应的安装命令如下：
```
npm install hexo-generator-sitemap --save
npm install hexo-generator-baidu-sitemap --save
```

### 了解 sitemap

sitemap：中文译为“站点地图”

什么是站点地图？

站点地图是一种文件，您可以通过该文件列出您网站上的网页，从而将您网站内容的组织架构告知 Google 和其他搜索引擎。Googlebot 等搜索引擎网页抓取工具会读取此文件，以便更加智能地抓取您的网站。

此外，站点地图能够提供与其中所列网页相关的宝贵元数据：元数据是网页的相关信息，例如此网页的上次更新时间、更改频率及其重要性（与相应网站中的其他网址相较而言）。

您可以使用站点地图向 Google 提供您网页上特定类型内容（包括视频和图片内容）的元数据。例如，您可以向 Google 提供有关视频和图片内容的信息：

站点地图视频条目可以指定视频的时长、类别和年龄适宜性分级。
站点地图图片条目中可包含图片主题、类型和许可。

## 修改站点配置文件 `_config.yml`

1. 添加如下的配置（注意每行的空格）
```
# sitemap
sitemap:
 path: sitemap.xml
baidusitemap:
 path: baidusitemap.xml
```

2. 找到原URL的部分，并修改为自己的博客网址，如下：
```
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://yoursite.github.io
```

3. 修改文章链接，在上述步骤2的url下方，找到关键字 `permalink`，并修改为如下形式：
```
permalink: :title/
```

4. 在博客根目录中的 source 文件夹下，添加蜘蛛协议 “robots.txt” 的文件，内容如下：
```
User-agent: *
Allow: /
Allow: /categories/
Allow: /tags/
Allow: /archives/
Allow: /about/

Disallow: /vendors/
Disallow: /js/
Disallow: /css/
Disallow: /fonts/
Disallow: /vendors/
Disallow: /fancybox/

Sitemap: http://yoursite.github.io/sitemap.xml
Sitemap: http://yoursite.github.io/baidusitemap.xml
```

### 基于 NexT 主题的首页 title 优化

如果恰巧你也使用的是NexT主题，那么可以参照如下的方式进行首页 title 优化。这并非必要，可因个人喜好而自行决定是否修改。

对应修改文件的路径：your-hexo-site/themes/next/layout 下的 `index.swig` 文件。

找到上述 `index.swig` 文件中如下的代码片段：
```
{% block title %} {{ config.title }} {% endblock %}
```
然后修改其为如下代码：
```
{% block title %} {{ config.title }} - {{ theme.description }} {% endblock %}
```
如果做了SEO关键字的设定，也期望在首页 title 中显示的话，也可修改为如下的代码：
```
{% block title %} {{ theme.keywords }} - {{ config.title }}{{ theme.description }} {% endblock %}
```

## 基于 NexT 主题添加 nofollow 标签

**注：此项也并非必须要修改，非NexT主题也可忽略！！！**

nofollow标签是由谷歌领头创新的一个“反垃圾链接”的标签，并被百度、yahoo等各大搜索引擎广泛支持，引用nofollow标签的目的是：用于指示搜索引擎不要追踪（即抓取）网页上的带有nofollow属性的任何出站链接，以减少垃圾链接的分散网站权重。

rel这个属性它有许多的属性值，比如next、previous,、chapter、 section等等，比较常见的是 `rel='external nofollow'` 与 `rel='nofollow'` 两种参数的应用！

`rel='nofollow'` 属性是谷歌为了应对垃圾链接而引入的一个属性值，被各大搜索引擎引用！
`rel='external nofollow'` 只是更相对于 `rel='nofollow'` 参数更加规范一些而已！

`rel='external nofollow'` 与 `rel='nofollow'` 其功能的中文译文为“不要读取”或“外部链接不要读取”的意思！

* 第一步：修改 `footer.swig` 文件

找到位于：your-hexo-site/themes/next/layout/_partials/footer.swig 路径下的 `footer.swig`文件，打开后，找到如下的代码片段：
```
{{ __('footer.powered', '<a class="theme-link" href="https://hexo.io">Hexo</a>') }}
```
将其修改为：
```
{{ __('footer.powered', '<a class="theme-link" href="http://hexo.io" rel="external nofollow">Hexo</a>') }}
```
接下来，继续找到如下代码片段：
```
<a class="theme-link" href="https://github.com/iissnan/hexo-theme-next">
```
将其修改为：
```
<a class="theme-link" href="https://github.com/iissnan/hexo-theme-next" rel="external nofollow">
```

* 第二步：修改 `sidebar.swig` 文件

找到位于：your-hexo-site/themes/next/layout/_macro/sidebar.swig 路径下的 `sidebar.swig`文件，打开后，找到如下的代码片段：
```
<a href="{{ link }}" target="_blank" title="{{ name }}">
```
修改为：
```
<a href="{{ link }}" target="_blank" title="{{ name }}" rel="external nofollow">
```
接下来，继续找到如下代码片段：
```
<a href="https://creativecommons.org/{% if theme.creative_commons === 'zero' %}publicdomain/zero/1.0{% else %}licenses/{{ theme.creative_commons }}/4.0{% endif %}/" class="cc-opacity" target="_blank">
```
将其修改为：
```
<a href="https://creativecommons.org/{% if theme.creative_commons === 'zero' %}publicdomain/zero/1.0{% else %}licenses/{{ theme.creative_commons }}/4.0{% endif %}/" class="cc-opacity" target="_blank" rel="external nofollow">
```

----

# Google 收录

----

1. 登录 Google Search Console [Google 网站站长](https://www.google.com/webmasters/)

2. 添加我们的博客站点
{% asset_img search1.png %}

3. 进行验证：验证方式有多种，此处我们以“HTML标记”为例：选择HTML标记后，会有一段代码，我们将代码中的`content`所对应的值进行复制，找到我们的主题配置文件，找到关键字`google_site_verification`之后，将我们复制的值粘贴至此处（并取消注释）即可。
{% asset_img search2.png %}
{% asset_img search3.png %}
{% asset_img search4.png %}

4. 重新生成站点（完成上述所有的设定后）  
使用`hexo generate`重新生成我们的站点，为了保证有效生成，可在每次生成前，先进行清理：`hexo clean`。这个时候，我们便可以在Hexo的站点“public”文件夹中发现：sitemap.xml 与 baidusitemap.xml 的两个文件已经生成。

5. 部署新的站点  
将我们最新配置后并生成的站点（操作4所生成的站点），重新部署至 GitHubPages 上。

6. 部署后，此时在Goole中进行验证（建议部署后等待几十秒，以便部署生效后，再进行验证）
{% asset_img search5.png %}
{% asset_img search6.png %}

7. 验证成功后，在Google Search Console平台添加我们的站点地图
{% asset_img search7.png %}

8. 添加Google抓取：我们以抓取首页为例，直接点击抓取按钮即可看到抓取结果
{% asset_img search8.png %}

9. 将抓取通过的地址，进行请求编入索引（我们以博客首页加入抓取索引为例）
{% asset_img search9.png %}

10. 编入索引后，打开Google进行搜索（以博主的博客为例，搜索“tyousf”），确认结果：
{% asset_img search10.png %}

----

# 结语

----

由于也是各种探索和尝试中进行的，难免有所纰漏，如果有问题，欢迎大家在下方留言处多多指正。

在尝试过程中，博主也是找了很多的资料，其中各种描述，看的也是云里雾绕！经过自己亲自实践后，整编成本文！其中已经做了很多的修正。不过当然要感谢每一个我参考过资料的作者，没有他们的贡献，我也不可能这么快的实现SEO。

总结起来我们必须要做如下的事情进行基本的SEO：

* 安装 Sitemap 支持的包
* 配置 sitemap 的代码
* 修改 URL 为站点地址
* 优化文章链接 permalink
* 添加蜘蛛协议 robots.txt
* 搜索引擎站长网站进行网站收录
 * 验证站点
 * 添加站点地图
 * 添加编入索引

接下来，让我们自己动手，添加百度收录吧！！！
附上百度站长平台传送门：[百度站长平台](http://zhanzhang.baidu.com/site/index)

----

# 参考资源

----

> [sitemap](https://support.google.com/webmasters/answer/156184?hl=zh-Hans&ref_topic=4581190)
> [SEO](https://zh.wikipedia.org/wiki/%E6%90%9C%E5%B0%8B%E5%BC%95%E6%93%8E%E6%9C%80%E4%BD%B3%E5%8C%96)
