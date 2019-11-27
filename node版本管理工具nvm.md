#### nvm 还是 n
> nvm有点类似于 Python 的 virtualenv 或者 Ruby 的 rvm，
> 每个node版本的模块都会被安装在各自版本的沙箱里面（因此切换版本后模块需重新安装），
> 因此考虑到需要时常对node版本进行切换测试兼容性和一些模块对node版本的限制，我
> 选择了使用nvm作为管理工具，下面就来说说nvm的安装和使用过程。

#### 安装
`url -o-https://raw.githubusercontent.com/creationix/nvm/v0.30.2/install.sh | bash`
#### 配置
> 完成后nvm就被安装在了~/.nvm下啦，接下来就需要配一下环境变量了，  
> 如果你也使用了zsh的话，就需要在~/.zshrc这个配置文件中配置，
> 否则就找找看~/.bash_profile或者~/.profile吧。  
> 打开~/.zshrc，在最后一行加上：  
`export NVM_DIR="$HOME/.nvm"`
`[ -s"$NVM_DIR/nvm.sh"] && ."$NVM_DIR/nvm.sh"# This loads nvm`
> 这一步的作用是每次新打开一个bash，nvm都会被自动添加到环境变量中了。  
> 完成后输入source ~/.zshrc重新启动一下配置。

#### 命令

**nvm ls-remote**：列出所有可以安装的node版本号  
**nvm install v10.4.0**：安装指定版本号的node  
**nvm use v10.3.0**：切换node的版本，这个是全局的  
**nvm current**：当前node版本  
**nvm ls**：列出所有已经安装的node版本  
