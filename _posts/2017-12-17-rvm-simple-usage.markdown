---
layout: post
title:  "RVM simple usage"
date:   2017-12-17 12:55:30 +0800
categories: jekyll update
---
最好的建议是参考： [官方文档](http://jekyllcn.com/docs/home/)

- Jekyll 是一个简单的博客形态的静态站点生成器，Jekyll 生成的静态站点可以运行在任何你喜欢的服务器上，推荐的实用方式是运行在 GitHub Page 上

- 简单实用
 1. 安装：当前 Jekyll 3.0 要求 Ruby 2.0 及以上版本
 ```
 $ gem install jekyll
 ```
 2. 生成站点模版
 ```
 $ jekyll new myblog
 ```
 生成的 Jekyll 的模版模版如下：
 ```
 $ tree myblog/
 myblog/
├── 404.html
├── Gemfile
├── _config.yml
├── _posts
│   └── 2017-12-17-welcome-to-jekyll.markdown
├── about.md
└── index.md
 ```
 3. 安装 gem
 ```
  $ cd myblog/
  $ gem install bundler
  $ bundle install
 ```
  测试日志模版如下：
  ```
  $ tree myblog/
myblog/
├── 404.html
├── Gemfile
├── Gemfile.lock
├── _config.yml   # 配置文件
├── _includes   # 可以在布局和其他文章中引入的文件
├── _layouts    # 布局文件
├── _posts    # 文章放在这个目录下
│   └── 2017-12-17-welcome-to-jekyll.markdown
├── _site   # 编译后的文件
│   ├── 404.html
│   ├── about
│   │   └── index.html
│   ├── assets
│   │   └── main.css
│   ├── feed.xml
│   ├── index.html
│   └── jekyll
│       └── update
│           └── 2017
│               └── 12
│                   └── 17
│                       └── welcome-to-jekyll.html
├── about.md
├── index.html  # 入口文件
└── index.md
```
 4. 启动 Jekyll 开发服务器，实用浏览器预览
 ```
 $ jekyll serve
 ```
 服务默认启动在 4000 端口，文章内容回编译到当前目录下 `_site` 目录下。

 - 编辑器打开当前项目，编辑自己的第一片文章
 ```
 myblog/
├── 404.html
├── Gemfile
├── Gemfile.lock
├── _config.yml
├── _data
├── _includes
│   ├── footer.html
│   ├── head.html
│   ├── header.html
│   └── main.html
├── _layouts
│   ├── default.html
│   └── post.html
├── _posts
│   └── 2017-12-17-rvm-simple-usage.markdown
├── about.md
├── favicon.ico
├── index.html
└── index.md
 ```
 参考地址： [Demo](https://github.com/wewin11235/jekyll-demo)

 - 使用 GitHub Pages 发布
 1. GitHub 上创建用于发布 Blog 的仓库，将 Jekyll 项目 push 到该仓库
  比如我创建的仓库为：'wewin11235/myblog'
 3. 仓库管理，进入 Settings ，启用 GitHub page
