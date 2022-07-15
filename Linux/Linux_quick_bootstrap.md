# Linux quick bootstrap

## Aliyun_server_info

> ip:   47.106.86.12

open port

- 4000  //butterfly
- 20/21 //ftp
- 22    //ssh


## Basic configuration

### Initialize
``` bash
# replace default apt source(optional)

$ sudo apt update && sudo apt upgrade

# installation
$ sudo apt install vim-gtk  # or other vim version that support register "* and "+
# otherwise you need modify vimrc to change the performance of y and p 
$ sudo apt install build-essential git tmux unzip cmake trash-cli
$ sudo apt install net-tools openssh-server
$ sudo apt install zsh  # highly recommended, ultimate powerful shell
$ sudo apt update && sudo apt upgrade

# configure ssh service
$ services sshd status
$ services ufw allow ssh  # ufw refers to ubuntu firewall
$ services sshd start

# change hostname(optional)
$ vim /etc/hostname  # reboot to take effect

# uninstall FireFox(optional)
$ sudo apt remove --purge $(dpkg -l | grep firefox)
```


### Add user
``` bash
$ sudo useradd -c "Comment for this user(optional)" -d [user dir] [user name]
$ sudo passwd [user name]

# make login directory && shell for new user
$ sudo mkdir [user dir] && sudo chown -cR eric:eric [user dir]

$ sudo vim /etc/sudoers         # make as powerful as super suer, use it carefully!
# or simply add user to /etc/sudoers.d(recommended)

$ su [user name]
$ chsh -s $(which zsh)
```


### Ftp
``` bash
$ sudo apt install  vsftpd

$ systemctl  status vsftpd.service
$ systemctl  start vsftpd.service          //open port 20/21
$ systemctl  stop vsftpd.service
# restart this service if can't transport file to Linux

$ vim /etc/vsftpd.conf
# write_enable=NO改为write_enable=YES，这样权限就运行了

$ put <url - local> <url - remote>
$ get <url - local> <url> - remote
```


### Customize zsh with ohmyzsh
```bash
# install ohmyzsh into $HOME/.local/share/oh-my-zsh
$ git clone --depth 1  https://github.com/robbyrussell/oh-my-zsh.git $HOME/.local/share/oh-my-zsh

# set temporary ZSH env
$ export ZSH="$HOME/.local/share/oh-my-zsh"
$ export ZSH_CUSTOM="$ZSH/custom"

# zsh plugins
# zsh-syntax-highlighting
$ git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
# zsh-autosuggestions
$ git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
# git-open(optional)
$ git clone https://github.com/paulirish/git-open.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/git-open
```


### Link dotfiles
``` bash
# ---* Attention *---
# don't run this blindly unless you are aware of what effect it will take
# ---*  *---
# generate asymmetrical key, use rsa algorithm(widely used) or ed25519(new and powerful)
$ ssh-keygen  -t  [ed25519]|[rsa]

# put your public key into github account

# test ssh connection and add github.com to you ~/.ssh/knownhost
$ ssh -T git@github.com

# clone configuration from github
$ git clone --depth 1  https://github.com/aeric777/dotfiles.git $HOME/Documents/dotfiles
$ cd $HOME/Documents/dotfiles && ./bootstrap.sh

# if .bashrc or .zshrc doesn't automatically work when you login
# $ vim ~/.bash_profile
# if [ -f ~/.bashrc ] ; then
#         source .bashrc
# fi

# relogin

# print 'unable to access  [URL]', when using git pull
$ git config --global --unset http.proxy
```


### VIM-Plugins
```bash
# if you don't need vim-plugins, comment the corresponding part in vimrc
# vim-plus, a minimalist Vim plugin manager.
$ curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
# using :PlugInstall in vim

# YouCompleteMe
# cd ~/.vim/plugged/YouCompleteMe
$ git submodule update --init --recursive
$ ./install.py --clang-completer
```

### Python
see [miniconda website](https://docs.conda.io/en/latest/miniconda.html).
``` bash
# highly recommend managing python env using miniconda environment
# Miniconda is a free minimal installer for conda
conda init  # initialize conda env
conda config --set changeps1 false
```

## other useful software
``` bash
# super cat
$ sudo apt install bat
$ mkdir -p ~/.local/bin && ln -s /usr/bin/batcat ~/.local/bin/bat
```


## Mysql
``` bash
# instal MySQL  using apt on Ubuntu
# See this [Page](https://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en/#apt-repo-fresh-install)
$ systemctl [`stop`,`start`, `status`, `restart`] mysql //operation on MySQL-server


# instal MySQL  using pip on Windows
$ pip install cryptography      //when using pymysql in python
```


## Nginx
``` bash
# 查找安装目录 method-1[]
$ ps -ef | grep nginx
# method-2
# 利用上面的命令查看nginx的PID，就用上面的16150，然后通过该进程ID来查找当前运行的nginx目录，命令如下
$ ll /proc/16150/exe
```


## Terraria server
``` bash
$ sudo mkdir /opt/terraria; cd /opt/terraria
$ sudo chown -cR eric:eric  /opt/terraria
$ mkdir bin worlds  zip

# extract corresponding file

# modify your configuration
```


## swap-todo
``` bash
# make swap
$ free -m       # check swap status
$ df -h         # check disk   status
```


## Hexo blog
``` bash
# Building blog with Hexo  注意看要求的软件版本

# install nodejs & git
# make sure you are using latest version of git
$ curl -fsSL https://deb.nodesource.com/setup_16.x | sudo -E bash -
$ sudo apt-get install -y nodejs

# make sure you have installed latest npm

# install hexo[https://hexo.io/zh-cn/docs/]

# theme/butterfly [https://butterfly.js.org/posts/21cfbf15/]

# Hexo command：
$ hexo init [folder]

$ hexo clean    # 更换主题之后，清除缓存文件 (db.json) 和已生成的静态文件 (public)。

$ hexo g        # 生成静态网页
$ hexo deploy   # 部署网站。

$ hexo new [layout] <title>     # 新建一篇文章。如果没有设置 layout 的话，默认使用 _config.yml 中的 default_layout 参数代替。如果标题包含空格的话，请使用引号括起来。

$ hexo publish [layout] <filename>      # 发表草稿。
$ hexo server                           # 启动服务器。默认情况下，访问网址为： http://localhost:4000/
```