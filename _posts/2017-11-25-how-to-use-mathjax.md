---
layout: post
title: 在github pages上添加mathjax支持
date: 2017-11-25
categories: blog
tags: [个人备忘]
description: 使用mathjax
---

星期六, 25. 十一月 2017 02:25下午 

在昨天发布[一种新型的深度结构-和积网络简介](http://willishu.cn/blog/2017/11/24/spn_from_tumblr/)时，发现添加的公式不能显示，于是搜了一下发现可能是mathjax支持没有开，[这里](在Octopress中使用LaTeX)找到了解决办法。

**Notice:本人使用的系统为ubuntu16.04，retext为2.6.1-1**

由于我是使用的github pages，直接fock他人的项目，因而在mygithub.github.io//_include//head.html文件中，在`<head></head>`之中添加了如下语句：

```
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      processEscapes: true
    }
  });
</script>

<script type="text/x-mathjax-config">
    MathJax.Hub.Config({
      tex2jax: {
        skipTags: ['script', 'noscript', 'style', 'textarea', 'pre', 'code']
      }
    });
</script>

<script type="text/x-mathjax-config">
    MathJax.Hub.Queue(function() {
        var all = MathJax.Hub.getAllJax(), i;
        for(i=0; i < all.length; i += 1) {
            all[i].SourceElement().parentNode.className += ' has-jax';
        }
    });
</script>

<script type="text/javascript"
   src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
```

之后在github上提交更改，发现页面可以支持公式显示。

之后由于本地使用的是retext编辑markdown文件，实时预览时仍然不能显示，查到[这里](https://github.com/retext-project/retext/wiki/Math)有提示要先安装mathjax，之后在retext软件菜单内点击**编辑**$\rightarrow $**个人偏好**$\rightarrow $**markdown语法扩展**内添加mathjax，再选择**编辑**$\rightarrow $**使用webkit渲染**，即可以显示。
