# webpack


## webpack的优点
1. 支持多种模块标准
2. 具有完备的代码分割(code-splitting)解决方案
3. 处理各类型资源
4. 拥有活跃的社区，大量的插件和工具


## webpack的安装
webpack安装可分为全局安装和本地安装，推荐本地安装，因为在使用webpack插件时，会依赖项目中的webpack的内部模块。为了避免混洗，不要在全局和本地都安装webpack。安装：`npm install -S webpack webpack-cli`，webpack是核心模块，webpack-cli是命令行工具。使用npx执行webpack，验证安装状态，`npx webpack -v`，`npx webpack-cli -v`;

## webpack基本JS解析功能
npm script 命令：`webpack --entry=./index.js --output-filename=bundle.js --mode=development`，指定入口文件和出口文件，默认入口当前目录下的index.js,出口目录默认是当前目录下生成dist，通过`npx webpack -h`,查看更多webpack命令，最终编译过后的JS是浏览器能识别的。为了能够满足前端各种各样的工程配置，通过定义webpack提供的webpack.config.js文件，编写符合文档规范的配置，在npm script中的webpack命令默认解析webpack.config.js文件配置。

## webpack-dev-server
每次执行webpack命令后，生成新的编译文件，切回浏览器后，都需要手动刷新，为了解决这个问题，社区提供了webpack-dev-server，安装`npm install webpack-dev-server -S`,**-S**参数表明在开发阶段用到该工具或者称为库，便于开发和调试，上线安装依赖时，通过命令`npm install --production`,过滤devDependencies的冗余模块，加快安装和发布速度;在npm script 命令脚本中添加命令"dev":"webpack-dev-server",另外webpack.config.js中也需要配置devServer字段：
```

devServer:{
    publicPath:"/dist",
}

```
webpack-dev-server相当于一个服务，主要工作接受浏览器请求，然后将资源返回。整体流程，服务启动(默认将项目挂载在localhost:8080)：先命令webpack从入口开始打包文件（打包文件默认在根目录上），打包好的资源都是存放在内存中的，而不是本地磁盘；webpack-dev-server接受到浏览器资源请求时，进行URL地址校验，如果该地址是资源服务地址，即publicPath所配置的地址，将在webpack打包结果中寻找该资源送给浏览器，如果请求地址不属于资源服务地址，则直接从硬盘中读取源文件送给浏览器。webpack-dev-server提供便捷特性live-reloading（自动刷新）。

# 模块打包