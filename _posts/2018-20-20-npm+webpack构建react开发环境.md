---
layout: post
title: react 开发环境构建
date: '2018-02-20 07:35:30 +0800'
---

- 创建项目目录
  ```
  $ mkdir test
  $ cd test
  ```
- 使用 npm 包管理工具
  ```
  $ npm init // 初始化 npm 环境
  ```
- 安装 webpack 打包工具
  ```
  $ npm install -g webpack // 全局安装 webpack
  $ npm install webpack --save-dev // 开发环境安装 webpack
  ```
- 热加载模块
  ```
  $ npm install webpack-dev-server --save-dev
  ```
- 安装 react react-dom 模块
  ```
  $ npm install react react-dom --save-dev
  ```
- react 使用 es2015 语法需要使用babel-loader
  ```
  $ npm install babel-core babel-loader babel-preset-es2015 babel-preset-react --save-devss
  ```
- 创建示例项目基本目录
  ```
  .
  ├── dist // 打包输入位置，可以不建立
  │   ├── index.html
  │   └── main.js
  ├── package-lock.json
  ├── package.json
  ├── src // 源文件位置
  │   └── index.js
  └── webpack.config.js // webpack 配置文件
  ```
- 示例代码

  ./src/index.js:
  ```
  import React from 'react';
  import ReactDOM from 'react-dom';

  ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('root')
  );

  ```
  ./dist/index.html
  ```
  import React from 'react';
  import ReactDOM from 'react-dom';

  ReactDOM.render(
    <h1>Hello, world!</h1>,
    document.getElementById('root')
  );
  weiweideMacBook-Pro:05-01 wewin$ cat dist/index.html
  <div id="root"></div>

  <script src="/main.js" charset="utf-8"></script>
  ```
- 配置 webpack
  ```
  const path = require('path');
  const webpack = require('webpack');

  const config = {
    entry: './src/index.js', // 入口文件
    output: {
      path: path.resolve(__dirname, 'dist'),  // 出口文件
      filename: 'main.js' // js 输出文件
    },
    module: {
      loaders: [
        {
          test: /\.jsx?$/,
          loader: 'babel-loader', //babel-loader 解析 es2015 和 jsx 语法
          exclude: /node_modules/,
          query: {
            presets: ['es2015', 'react'] //解析 es2015 和 jsx 语法
          }
        }
      ]
    },
    plugins: [
      new webpack.HotModuleReplacementPlugin() // 热加载组建
    ],
    devServer: {   // webpack-dev-server 相关配置
      contentBase: path.join(__dirname, "dist"), // 使用 dist 下的 index.html 作为打开开的主页
      compress: true,  // 压缩 dist
      port: 9000, // 端口
      open: true, // 打开浏览器
      inline: true // webpack-dev-server 的运行模式，js 更醒后自动刷新浏览器
    }
  };

  module.exports = config;
  ```

- 启动 dev server
  ```
  $ webpack-dev-server
  ```
  启动可以看到页面上显示 hello world。react 开发环境基本构建完成

- 编辑 package.json 创建启动脚本
  ```
  {
    ....

    "scripts": {
      "start": "webpack-dev-server", // webpack-dev-server 启动脚本
    }
    ....
  }
  ```
  此时可以使用下面命令启动 dev server
  ```
  npm run start
  ```
- react css module
  ```
  $ npm install css-loader style-loader --save-dev
  ```

- 内联样式表达式:
  const HeaderStyle = {
    header: {
      color: this.status.is_red ? 'red' : 'green'
    }
  }
- react component className to class
  ```
  $ npm install babel-plugin-react-html-attrs
  ```

- css 在线转化为 react 需要那个的 css

- css 模块化使用 变量

- use ant design
  ```

  ```

- react router
  ```
  $ npm install react-router
  ```
