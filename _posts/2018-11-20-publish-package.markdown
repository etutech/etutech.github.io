---
layout: post
title:  "发布 package 到 npm （React 组件库）"
date:   2018-11-20 09:11:00 +0800
categories: frontend
---

### 基本步骤

- 前提
  - npmjs.com 的账号，在本机登录 `npm login`
  - 项目根文件夹下 package.json 中的 name 和 version 对应 npm 包名及 包版本号
  - package.json 内的 main 指向的就是被引入的入口文件
  
- 发布
  ```
  $ npm build
  $ npm publish
  ```

### 踩过的坑

- 如果包名为 **@org/blurblur** 此类的包发布时 需要
  ```
  $ npm publish --access=public
  ```

- 如果设置过 npm 淘宝镜像， 需要设置回 npmjs 的镜像 
  ```
  $ npm config set registry http://registry.npmjs.org
  ```

- 遇到 418 error， 清理下 proxy 
  ```
  $ npm config delete proxy
  $ npm config delete https-proxy
  ```

### 创建 React 组件库 并发布到 npm  
参考自 [如何创建 React 组件并发布到 npm](https://juejin.im/post/5ab4947a6fb9a028bc2dac99)

**注意点**
- 本地开发为了方便测试，可以在库项目下使用 `yarn link`, 然后在使用该库的其他项目下 `yarn link 包名` 关联 （电脑重启后，需重新做此两步操作）

- webpack 配置文件中 output 内 libraryTarget 可选 amd, umd, commonjs, commonjs2 等， 使用 esm 的项目建议 commonjs2

- 如果是共有库(使用该库的其他项目已安装该依赖)，比如 antd, lodash, 此类依赖需要在 webpack 配置文件中设置 externals
  ```
  {
    externals: {
      "styled-components": "styled-components",
      "react": "react",
      "react-dom": "react-dom",
      "antd": "antd",
      "prop-types": "prop-types"
    }
  }
  ```  

### 参考资料

- [轻松发布 react 组件到 npm](https://juejin.im/post/5beb0fb6f265da61441f9a9c)
- [如何创建 React 组件并发布到 npm](https://juejin.im/post/5ab4947a6fb9a028bc2dac99)
