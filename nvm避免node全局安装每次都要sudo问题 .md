### nvm避免node全局安装每次都要sudo问题
#### 准备
查看已经安装在全局的模块，以便删除这些全局模块后再按照不同的 node 版本重新进行全局安装
```bash
npm ls -g --depth=0
```

删除之前的全局 node_modules 目录
```bash
sudo rm -rf /usr/local/lib/node_modules
```

删除 node
```bash
sudo rm /usr/local/bin/node
```

删除全局 node 模块注册的软链
```bash
cd /usr/local/bin && ls -l | grep "../lib/node_modules/" | awk '{print $9}'| xargs rm
```

使用nvm
```bash
nvm install stable # 安装最新稳定版 node，现在是 5.0.0
nvm install 4.2.2 # 安装 4.2.2 版本
nvm install 0.12.7 # 安装 0.12.7 版本
nvm use 4 # 切换至 4.2.2 版本
npm install -g mz-fis # 安装 mz-fis 模块至全局目录，安装完成的路径是 /Users/<你的用户名>/.nvm/versions/node/v0.12.7/lib/mz-fis
nvm use 0 # 切换至 0.12.7 版本
npm install -g react-native-cli #安装 react-native-cli 模块至全局目录，安装完成的路径是 /Users/<你的用户名>/.nvm/versions/node/v4.2.2/lib/react-native-cli
nvm alias default 0.12.7 #设置默认 node 版本为 0.12.7
```

umi路径
```bash
/Users/[name]/.nvm/versions/node/[版本]/lib
```

切换版本重新安装依赖
但问题来了，我们安装过的 npm 包，都要重新再装一次？幸运的是，我们有个办法来解决我们的问题，运行下面这个命令，可以从特定版本导入到我们将要安装的新版本 Node：

```bash
nvm install v5.0.0 --reinstall-packages-from=4.2
```

参考
https://www.jianshu.com/p/04d31f6c22bd
