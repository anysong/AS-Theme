#### nvm 还是 n
> nvm有点类似于 Python 的 virtualenv 或者 Ruby 的 rvm，
> 每个node版本的模块都会被安装在各自版本的沙箱里面（因此切换版本后模块需重新安装），
> 因此考虑到需要时常对node版本进行切换测试兼容性和一些模块对node版本的限制，我
> 选择了使用nvm作为管理工具，下面就来说说nvm的安装和使用过程。

#### nvm
github地址: **https://github.com/nvm-sh/nvm**
#### 安装&更新
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
```
#### 官方不建议用brew安装nvm 如已经安装建议卸载
```bash
Homebrew installation is not supported. If you have issues with homebrew-installed nvm, please brew uninstall it, and install it using the instructions below, before filing an issue.
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

`nvm ls-remote`：列出所有可以安装的node版本号  
`nvm install v10.4.0`：安装指定版本号的node  
`nvm use v10.3.0`：切换node的版本，这个是全局的  
`nvm current`：当前node版本  
`nvm ls`：列出所有已经安装的node版本  
```bash
Example:
  nvm install 8.0.0                     Install a specific version number
  nvm use 8.0                           Use the latest available 8.0.x release
  nvm run 6.10.3 app.js                 Run app.js using node 6.10.3
  nvm exec 4.8.3 node app.js            Run `node app.js` with the PATH pointing to node 4.8.3
  nvm alias default 8.1.0               Set default node version on a shell
  nvm alias default node                Always default to the latest available node version on a shell
```
