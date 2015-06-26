---
layout: post
title: 使用第三方评论系统：多说
tags: github
category: 技术
---
## 为博客增加评论功能 ##
使用第三方评论插件“多说”，顺便也试试MarkdownPad 2编辑md文件.

### Disqus ###

博客默认的评价插件是disqus，但是这东西是国外的，有的时候不是很稳定，还是支持一下国产的软件，可以用微博、QQ、人人、豆瓣等帐号登录并评论。.


### 多说 ###

来吧，直接上步骤：

- 首先是要注册多说账号了，http://duoshuo.com/，首页点击我要安装，相当于注册。
- 注册的时候注意“站点名称”这个选项，后面各种配置需要用到。
- 注册好了之后，网站会自动生成一段通用的代码，这里主要看第一行：

		<div class="ds-thread" data-thread-key="{{ page.id }}" data-title="{{ page.title }}" data-url="{{ site.url }}{{ page.url }}"></div>

     data-thread-key.data-title.data-url三个参数修改成代码中的样子。

- 代码修改后，在项目的_includes文件中增加一个文件，名称为duoshuo_comments.html，文件中的内容即为上一步修改的代码。
- 在需要增加评论的地方增加代码：

		{-% include duoshuo_comments.html %-} //去掉-

    即完成评论的增加。

    但是我们会惊奇的发现...不支持动态载入，当切换页面了之后，评论框就不见了，除非手动刷新...

### 动态载入 ###

万能的百度啊，不用吐槽，单位上不了谷歌...

查找到了动态载入的方法，步骤如下：

- 在主js文件中增加方法：

		function toggleDuoshuoComments(container){
			var el = document.createElement('div');//该div不需要设置class="ds-thread"
			el.setAttribute('data-thread-key', '{{ page.id }}');//必选参数
			el.setAttribute('data-url', '{{ site.url }}{{ page.url }}');//必选参数
			el.setAttribute('data-author-key', 'liuweigg');//可选参数
			DUOSHUO.EmbedThread(el);
			jQuery(container).append(el);
		}

  
在需要增加评论的地方，增加代码：

	<a href="javascript:void(0);" onclick="toggleDuoshuoComments('#comment-box');">展开评论</a>
    <div id="comment-box" ></div>

相当于增加了个链接，点击后载入评论框，但是这里...不知道是我设置的问题还是本身的BUG，多次点击链接，会多次加载评论框，于是就会有很多很多的评论框。

这里偷了个懒：

增加一个div，并且赋予ID

	  <div id="opencomment" ></div>

js的方法中，点击完了之后，自动让div隐藏

      oc.style.display="none";
      var oc = document.getElementById('opencomment');

