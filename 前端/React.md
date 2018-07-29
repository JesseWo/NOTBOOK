## 技术栈
- [react-developer-roadmap](https://github.com/adam-golab/react-developer-roadmap)
- [阮一峰: React 技术栈系列教程](http://www.ruanyifeng.com/blog/2016/09/react-technology-stack.html)

## 官方文档(cn)
- [官方文档(cn)](https://www.reactjscn.com/docs/hello-world.html)
- [react-router](https://reacttraining.com/react-router/web/guides/philosophy)

## CSS解决方案
- [CSS-Modules](https://github.com/css-modules/css-modules)
- [阮一峰: CSS Modules 用法教程](http://www.ruanyifeng.com/blog/2016/06/css_modules.html)
- [sass](https://www.sass.hk/guide/)

## Redux
- [官方文档](https://redux.js.org/)
- [Redux 入门教程（一）：基本用法](http://www.ruanyifeng.com/blog/2016/09/redux_tutorial_part_one_basic_usages.html)
- [Redux 入门教程（二）：中间件与异步操作](http://www.ruanyifeng.com/blog/2016/09/redux_tutorial_part_two_async_operations.html)
- [Redux 入门教程（三）：React-Redux 的用法](http://www.ruanyifeng.com/blog/2016/09/redux_tutorial_part_three_react-redux.html)

## 静态检查
- [TypeScript](https://www.tslang.cn/docs/home.html)

## 打包构建
- [webpack文档](https://www.webpackjs.com/concepts/)
- [入门 Webpack，看这篇就够了](https://segmentfault.com/a/1190000006178770)
- [webpack plugins](https://www.webpackjs.com/plugins/)
- [webpack-merge](https://github.com/survivejs/webpack-merge): 用于不同环境的webpack.config.js抽取.

### webpack 4.x 填坑

webpack 升级到4.3.x后, `ExtractTextWebpackPlugin` 会报
> Error: Path variable [contenthash] not implemented in this context: style/[name].[contenthash].css

具体参考 [issue763](https://github.com/webpack-contrib/extract-text-webpack-plugin/issues/763)
, 且未来 `extract-text-webpack-plugin` 将废弃, 作者推荐用 [mini-css-extract-plugin](https://github.com/webpack-contrib/mini-css-extract-plugin) 取代 [ExtractTextWebpackPlugin](https://www.webpackjs.com/plugins/extract-text-webpack-plugin/).

## 脚手架
- [create-react-app](https://github.com/facebook/create-react-app)
- [react-app-rewired](https://github.com/timarney/react-app-rewired)
    > 一种修改 `create-react-app webpack` 配置的社区解决方案, 不用 `eject` 也不用直接修改 `react-script`;

## node
- [npm官方文档](https://docs.npmjs.com/)
- [阮一峰: package.json](http://javascript.ruanyifeng.com/nodejs/packagejson.html)
- [npm scripts 使用指南](http://www.ruanyifeng.com/blog/2016/10/npm_scripts.html)

环境变量
- [process.env](http://nodejs.cn/api/process.html#process_process_env)
- [dotenv](https://github.com/motdotla/dotenv)
- [webpack 使用环境变量](https://www.webpackjs.com/guides/environment-variables/)

## 轮子
- [Ant Design of React](https://ant.design/docs/react/introduce-cn)
    ### antd中的坑
    - [babel-plugin-import: 按需加载antd中的组件和样式](https://github.com/ant-design/babel-plugin-import#usage)
    - [解决引入antd样式无效问题](https://www.jianshu.com/p/a25ba1adeda2)
    - [解决css-modules与antd冲突问题(antd样式不生效)](https://www.jianshu.com/p/51ff1c8be301)

- [二维码生成: qrcode.react](https://github.com/zpao/qrcode.react)
- [优秀轮子集锦](https://ant.design/docs/react/recommendation-cn)

## 优秀项目
- [react 后台管理系统解决方案](https://github.com/yezihaohao/react-admin)
- [使用 React 全家桶搭建一个后台管理系统](https://github.com/MuYunyun/reactSPA)