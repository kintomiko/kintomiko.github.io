---
layout: post
title: How to create new post using rakefile
date: 2016-04-29 10:23:26 +0800
categories: jekyll
---
RakeFile from https://github.com/chenxsan/chenxsan.github.io/blob/master/Rakefile

* 执行 rake new 命令
* 输入 URL，比如要创建 2014-11-12-sam-chen.md 文件，我们只需要输入 sam chen，当然，你也可以输入中文，但通常不建议
* 输入文章标题，即 .md 文件中 front matter 里的 title 的值
* 输入文章的分类，如果有多个分类，以空格分隔，比如 Jekyll zfanw 这样
* 最后，Rake 会启动 vi，打开新创建的 md 文件，当然，你也可以配置其他编辑器
