#### nvm 还是 n
> nvm有点类似于 Python 的 virtualenv 或者 Ruby 的 rvm，
> 每个node版本的模块都会被安装在各自版本的沙箱里面（因此切换版本后模块需重新安装），
> 因此考虑到需要时常对node版本进行切换测试兼容性和一些模块对node版本的限制，我
> 选择了使用nvm作为管理工具，下面就来说说nvm的安装和使用过程。

#### nvm
github地址: **https://github.com/nvm-sh/nvm**

#### 重要建议  
1. nvm不支持Windows 但有变通方法 详见官方文档 Note: nvm does not support Windows
2. Note: nvm does not support Fish
3. 如果你用zsh 可以安装zsh-nvm 通过run nvm upgrade to upgrade
4. 如果你安装了系统的node,并且想全局安装模块,注意以下几点:

+ When using nvm you do not need sudo to globally install a module with npm -g, so instead of doing sudo npm install -g grunt, do instead npm install -g grunt

+ If you have an ~/.npmrc file, make sure it does not contain any prefix settings (which is not compatible with nvm)

+ You can (but should not?) keep your previous "system" node install, but nvm will only be available to your user account (the one used to install nvm). This might cause version mismatches, as other users will be using /usr/local/lib/node_modules/* VS your user account using ~/.nvm/versions/node/vX.X.X/lib/node_modules/*

5. 官方不建议用brew安装nvm 如已经安装建议卸载
```bash
Homebrew installation is not supported. If you have issues with homebrew-installed nvm, please brew uninstall it, and install it using the instructions below, before filing an issue.
```
#### 安装&更新
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
```
```bash
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
```

#### 如果使用zsh 建议使用zsh-nvm
If you're using zsh you can easily install nvm as a zsh plugin. Install zsh-nvm and run nvm upgrade to upgrade.
##### [zsh-nvm](https://github.com/lukechilds/zsh-nvm)
```bash
# 手动安装
git clone https://github.com/lukechilds/zsh-nvm.git ~/.zsh-nvm

# 在~/.zshrc这个配置文件中配置
source ~/.zsh-nvm/zsh-nvm.plugin.zsh
```

#### 配置
``` bash

完成后nvm就被安装在了~/.nvm下啦，接下来就需要配一下环境变量了，
如果你也使用了zsh的话，就需要在~/.zshrc这个配置文件中配置，否则就找找看~/.bash_profile或者~/.profile吧。
打开~/.zshrc，在最后一行加上：

# nvm 配置
export NVM_DIR="$HOME/.nvm"

# 每次新打开一个bash，nvm都会被自动添加到环境变量中了。
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm

# Linux下命令补全工具bash-completion
# 安装 bash-completion 后，可用tab键补齐几乎任何内容，包括参数、文件、目录甚至包名等
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
完成后输入source ~/.zshrc重新启动一下配置。

```

#### 卸载
To remove nvm manually, execute the following:
```bash
# to remove, delete, or uninstall nvm - just remove the `$NVM_DIR` folder (usually `~/.nvm`)
$ rm -rf "$NVM_DIR"
```
Edit ~/.bashrc (or other shell resource config) and remove the lines below:
```bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
[[ -r $NVM_DIR/bash_completion ]] && \. $NVM_DIR/bash_completion
```

#### 使用系统原来的node
```bash
nvm use system
nvm run system --version
# 想要使用系统原来的node，运行nvm use system即可，
# 如果想要设置系统原来的node为默认运行的node，nvm alias default system 即可，
# 切换其他版本的node还是使用nvm use <版本号>
```

#### 命令
```bash
nvm ls-remote：列出所有可以安装的node版本号  
nvm install v10.4.0：安装指定版本号的node  
nvm use v10.3.0：切换node的版本，这个是全局的  
nvm current：当前node版本  
nvm ls：列出所有已经安装的node版本  

# Example:
nvm install 8.0.0                     Install a specific version number
nvm use 8.0                           Use the latest available 8.0.x release
nvm run 6.10.3 app.js                 Run app.js using node 6.10.3
nvm exec 4.8.3 node app.js            Run `node app.js` with the PATH pointing to node 4.8.3
nvm alias default 8.1.0               Set default node version on a shell
nvm alias default node                Always default to the latest available node version on a shell
```
#### 总结
+ nvm管理版本的好处是放便切换各个版本的node及其对应的全局依赖
+ nvm可以和系统原来的node共存 如果需要使用系统原来的node，运行`nvm use system`即可
+ 官方不建议用brew安装nvm 如已经安装建议卸载 `brew uninstall it`
+ 可以使用zsh-nvm 管理nvm版本 `nvm upgrade` If you want to upgrade to the latest release of nvm
