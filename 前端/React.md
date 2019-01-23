## 技术栈
- [react-developer-roadmap](https://github.com/adam-golab/react-developer-roadmap)
- [阮一峰: React 技术栈系列教程](http://www.ruanyifeng.com/blog/2016/09/react-technology-stack.html)

## 官方文档(cn)
- [官方文档(cn)](https://www.reactjscn.com/docs/hello-world.html)
- [react-router](https://reacttraining.com/react-router/web/guides/philosophy)
- [react-hot-loader](https://github.com/gaearon/react-hot-loader)
- [history](https://github.com/ReactTraining/history)

- [browserslist](https://github.com/browserslist/browserslist#queries)
    
    用于配置浏览器和node.js版本, 而且可以通用于各种前端工具:
    - Autoprefixer
    - Babel (external config in package.json or browserslist will be supported in 7.0)
    - postcss-preset-env
    - eslint-plugin-compat
    - stylelint-no-unsupported-browser-features
    - postcss-normalize

## Redux
- [官方文档](https://redux.js.org/)
- [redux中文文档](http://www.redux.org.cn/)
- [redux-actions](https://redux-actions.js.org/introduction/tutorial)
    - [Redux 入门教程（一）：基本用法](http://www.ruanyifeng.com/blog/2016/09/redux_tutorial_part_one_basic_usages.html)
    - [Redux 入门教程（二）：中间件与异步操作](http://www.ruanyifeng.com/blog/2016/09/redux_tutorial_part_two_async_operations.html)
    - [Redux 入门教程（三）：React-Redux 的用法](http://www.ruanyifeng.com/blog/2016/09/redux_tutorial_part_three_react-redux.html)
- [connected-react-router](https://github.com/supasate/connected-react-router)
    > A Redux binding for React Router v4

## Babel
> ES6, ES2017, TypeScript, CoffeScript等 => js
- [在webpack中集成: babel-loader](https://www.webpackjs.com/loaders/babel-loader/)
- [代码压缩/混淆/删除useless代码: UglifyJS2](https://github.com/mishoo/UglifyJS2/tree/harmony#output-options)

## CSS解决方案
- [CSS-Modules](https://github.com/css-modules/css-modules)
    - [阮一峰: CSS Modules 用法教程](http://www.ruanyifeng.com/blog/2016/06/css_modules.html)

- [sass](https://www.sass.hk/guide/)
    - [在webpack中集成: sass-loader](https://www.webpackjs.com/loaders/sass-loader/)
    - [sass-loader的依赖: node-sass](https://github.com/sass/node-sass)

- [postcss]()
    - [插件: Autoprefixer,浏览器兼容,自动添加前缀](https://www.npmjs.com/package/autoprefixer)
    - [在webpack中集成: postcss-loader](https://www.webpackjs.com/loaders/postcss-loader/#syntaxes)

## 静态检查
- [TypeScript](https://www.tslang.cn/docs/home.html)

## 打包构建
- [webpack文档](https://www.webpackjs.com/concepts/)
- [入门 Webpack，看这篇就够了](https://segmentfault.com/a/1190000006178770)
- [webpack plugins](https://www.webpackjs.com/plugins/)
- [webpack-merge](https://github.com/survivejs/webpack-merge): 用于不同环境的webpack.config.js抽取.

### webpack 4.x 填坑

webpack 升级到4.3.x后, `ExtractTextWebpackPlugin` 会报
> Error: Path variable [contenthash] not implemented in this context: style/[name].[contenthash].css

具体参考 [issue763](https://github.com/webpack-contrib/extract-text-webpack-plugin/issues/763)
, 且未来 `extract-text-webpack-plugin` 将废弃, 作者推荐用 [mini-css-extract-plugin](https://github.com/webpack-contrib/mini-css-extract-plugin) 取代 [ExtractTextWebpackPlugin](https://www.webpackjs.com/plugins/extract-text-webpack-plugin/).

## 脚手架
- [create-react-app](https://github.com/facebook/create-react-app)
- [react-app-rewired](https://github.com/timarney/react-app-rewired)
    > 一种修改 `create-react-app webpack` 配置的社区解决方案, 不用 `eject` 也不用直接修改 `react-script`;

环境变量
- [process.env](http://nodejs.cn/api/process.html#process_process_env)
- [dotenv](https://github.com/motdotla/dotenv)
- [webpack 使用环境变量](https://www.webpackjs.com/guides/environment-variables/)

## 轮子
- [Promise解决方案: bluebird](http://bluebirdjs.com/docs/getting-started.html)
- [Ant Design of React](https://ant.design/docs/react/introduce-cn)
    ### antd中的坑
    - [babel-plugin-import: 按需加载antd中的组件和样式](https://github.com/ant-design/babel-plugin-import#usage)
    - [解决引入antd样式无效问题](https://www.jianshu.com/p/a25ba1adeda2)
    - [解决css-modules与antd冲突问题(antd样式不生效)](https://www.jianshu.com/p/51ff1c8be301)

- [优秀轮子集锦](https://ant.design/docs/react/recommendation-cn)
