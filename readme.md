git 仓库地址：https://github.com/alex4524/bskF2e.git

## 目的：  新建一个 common 组件库 & 工具库

1. 组件：
   表格 表单

2. 工具：
   处理数据 resize someTools

3. Services

> 提供的使用方式

`npm i xx -S`

## 步骤

### lerna 管理 单一仓库 多个包

首先全局安装 lerna 工具  
`npm i lerna -g`  
用 lerna 工具初始化一个单库多包的项目  
`lerna init`

创建名字子包 bsk-util 和 bsk-ui-design  
`lerna create bsk-util`  
`lerna create bsk-ui-design`

给 scope 的子包添加依赖包，不加 scope 则是给所有子包添加依赖

`lerna add <package>[@version] [--dev] [--exact] [--peer]`

给指定子包安装依赖：  
比如

- 给 bsk-util 安装 moment 到 dependencies  
  `lerna add moment --scope=bsk-util`
- 给 bsk-ui-design 安装 vue 到 dependencies  
  `lerna add vue --scope=bsk-ui-design`
- 安装@babel/core 到 devDependencies  
  `lerna add @babel/core --scope=bsk-ui-design --dev`
- 给所有子包安装 rollup（到 devDependencies）：  
  `lerna add rollup --dev`
- 安装所有 packages 下的包的依赖  
  `lerna bootstrap`

一次遍历执行所有子包的 npm run build
`Lerna run build`

[所有 lerna 指令参考](http://www.febeacon.com/lerna-docs-zh-cn/routes/commands/)

### 发布到 npm 官方源

首先将 npm 包切换到 官方源,比如  
`npm config set registry https://registry.npmjs.org/`

[Npm 发包 遇到的问题 & 详细步骤文档参考](https://segmentfault.com/a/1190000017463371)

lerna publish 则为使用 lerna 即遍历所有子包，挨个执行 npm publish

注意每次发布新版本的包 必须升级 package.json 中的版本号

本地调式 npm 包：
可以在 lerna 项目中新建 demo 子包项目 专门用于调试
目录结构为：

--packages  
----bsk-utils  
----bsk-ui  
----demo
