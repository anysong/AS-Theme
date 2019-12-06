### Vue-cli3搭建项目

#### 安装node环境
Vue CLI 需要 Node.js 8.9 或更高版本. 推荐使用`nvm`管理node版本

#### 全局安装vue-cli3
在命令行执行
```bash
npm install -g @vue/cli@3
```
接下来我们在命令行运行
```bash
vue create vue-demo
```
这时候它会提醒我们来选择需要安装的选项
```bash
Vue CLI v3.12.1
┌───────────────────────────┐
│  Update available: 4.1.1  │
└───────────────────────────┘
? Please pick a preset: (Use arrow keys)
❯ default (babel, eslint) 
  Manually select features 
```
初次搭建，选择 Manually select features
选择 Babel Router Vuex CSS Pre-processors （使用空格键选中） 进行下一步插件配置
```bash
Vue CLI v3.12.1
┌───────────────────────────┐
│  Update available: 4.1.1  │
└───────────────────────────┘
? Please pick a preset: Manually select features
? Check the features needed for your project: (Press <space> to select, <a> to toggle all, <i> to invert selection)
❯◉ Babel
 ◯ TypeScript
 ◯ Progressive Web App (PWA) Support
 ◉ Router
 ◉ Vuex
 ◉ CSS Pre-processors
 ◯ Linter / Formatter
 ◯ Unit Testing
 ◯ E2E Testing
```

配置完成后就开始安装了 `注意`:安装过程可能会有各种报错,请参考[报错](https://github.com/anysong/AS-command/blob/master/%E6%8A%A5%E9%94%99.md)来解决, 等待安装完毕后执行
```bash
$ cd vue-demo
$ npm run serve
```
