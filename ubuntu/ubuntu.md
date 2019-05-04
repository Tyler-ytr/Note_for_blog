<!-- # ubuntu复活记
这是我今天第四次重装ubuntu,心情非常悲痛;
- 之前崩的原因是搜狗输入法安装的时候没有提前安装fcix框架,导致乱码然后系统就傻掉了;
- 重装很多次的原因是因为没有在重装之前完全的格式化分区,我建议每一次玩具坏了都要用windows格式化一次呜呜呜
- 下面是正式的复活操作:
-   sudo passwd(修改sudo密码)
    sudo apt-get update
   sudo apt-get install vim
- 更换国内源,我选的是清华源;
  https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/
  sudo vim /etc/apt/sources.list
  然后copy-paste;
  然后sudo apt-get update
  sudo apt-get upgrade
- 然后安装搜狗输入法(之前几次都因为它炸了我不信了……)
  https://blog.csdn.net/qq_33159059/article/details/85019467
  参考了上述blog;
- 然后搭建基本的环境,主要参考的PA讲义：
  su
  apt-get install build-essential
  apt-get install man                # on-line reference manual
  apt-get install gcc-doc            # manual for GCC
  apt-get install gdb                # GNU debugger
  apt-get install git                # reversion control system
  apt-get install libreadline-dev    # a library to use compile the project later
  apt-get install libsdl2-dev        # a library to use compile the project later
  apt-get install qemu-system-x86    # QEMU

- 然后安装chrome，配置小飞机;
  chrome bing 搜索就行啦
  我有gmail帐号,所以同步的很舒服

- 小飞机:
  我选择的是shadowsocks-libev(因为之前炸了好多次qt5以及普通的shadowsocks）:
  mkdir shadowsocks
  cd shadowsocks
  touch shadowsocks.json
  vim shadowsocks.json
  {
    "server":"my\_server\_ip",
    "server_port":53450,
    "local_address": "127.0.0.1",
    "local_port":1080,
    "password":"密码",
    "timeout":300,
    "method":"aes-256-gcm",
    "fast_open": false
  }
  然后ss-local -c ~/shadowsocks/shadowsocks/json & 
  自己测试一下;
  然后写一个自启动脚本
  touch ~/.ssstart.sh
  vim ~/.ssstart.sh
  内容是:
    #!/bin/bash
    ss-local -c ~/shadowsocks/shadowsocks.json &
  然后vim ~/.bashrc
  在末尾添加:
  alias ss='. ~/.ssstart.sh'
  :q
  退出vim之后：
  source ~/.bashrc
  尝试一下ss,熟悉的界面出现啦！



- 网易云音乐终于更新啦,上官网直接下载就行了,不需要骚操作啦
- 安装vscode
- 然后就是配置环节，主要配置zsh,tmux,还有vim;
- zsh:
  - https://www.sysgeek.cn/install-zsh-shell-ubuntu-18-04/  https://segmentfault.com/a/1190000013612471
  - 感谢何伟的配置
  - sudo apt-get update
	sudo apt-get install zsh
	chsh -s /bin/zsh (设置zsh为默认)
	重启计算机,你会发现你的终端变了
  - 安装oh-my-zsh插件
    wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh
  - 不改theme一无所有
	- 准备使用powerline主题
	- 首先安装字体：
	  git clone https://github.com/powerline/fonts.git --depth=1
    \# install
    cd fonts
    ./install.sh
    \# clean-up a bit
    cd ..
    rm -rf fonts
	- 安装完字体之后要记得使用：终端-编辑-首选项-文本-文本外观-自定义字体打勾-选一个带有powerline的	
	- 然后vim ~/.zshrc 改配置
	- 安装powerline:sudo apt install powerline 
	- 我的配置见文件夹的.zshrc	
	- 颜色选择困难请：for code ({000..255}) print -P -- "$code: %F{$code}This is how your text would look like%f"
	- 改完之后记得source ~/.zshrc
- tmux:
	- 我使用啦何伟的配置,具体见setting;
- vim:spf13-vim 懒人vim
  进入setting目录;
  bash spf13-vim.sh
  (何伟nb！)
  - 这个时候的vim没有办法和系统剪切版交互,我根据https://www.cnblogs.com/memory4young/p/could-not-use-system-clipboard-in-vim.html
  下载了其他一些插件:
    sudo apt-get install vim-scripts vim-gtk vim-gnome
  这样 vim --version|grep "cliboard"会看到+clipboard;
  然后就可以用+y,+p实现系统剪切版和vim剪切版的交互啦！
- OSlab还需要:
  - sudo apt-get install curl
  - sudo apt-get install  gcc-multilib
- git 配置请搜索廖雪峰 -->
# Ubuntu 配置记录
这是我今天第四次重装ubuntu,心情非常悲痛;
## 反思
-   之前崩的原因是搜狗输入法安装的时候没有提前安装fcix框架,导致乱码然后系统就傻掉了;
-   重装很多次的原因是因为没有在重装之前完全的格式化分区,我建议每一次玩具坏了都要用windows格式化一次呜呜呜

## 复活操作

#### 基本配置
- 管理员权限,换源,安装vim
    <pre><code>  sudo passwd(修改sudo密码)
    sudo apt-get update
    sudo apt-get install vim
    </code></pre>
-   更换国内源,这里我选择的是[清华源](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/)用下面的命令打开文件,并且注释里面的所有内容,
     <pre><code> sudo vim /etc/apt/sources.list
    </code></pre> 
    -   然后粘贴下面的内容到打开的文件里面
    <pre><code># 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
    deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
    deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
    deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
    deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
    </code></pre>
    如果你学过vim,就知道:w :q的含义,如果没有可以在终端使用vimtutor学习一下;
-   安装搜狗输入法(之前几次都因为它炸了我不信了……)，我参考了这一篇[博客]( https://blog.csdn.net/qq_33159059/article/details/85019467)
-   然后搭建基本的C语言环境,主要参考啦蒋老师的PA讲义
    <pre><code>su
    apt-get install build-essential
    apt-get install man                # on-line reference manual
    apt-get install gcc-doc            # manual for GCC
    apt-get install gdb                # GNU debugger
    apt-get install git                # reversion control system
    apt-get install libreadline-dev    # a library to use compile the project later
    apt-get install libsdl2-dev        # a library to use compile the project later
    apt-get install qemu-system-x86    # QEMU
    </code></pre>
-   安装chrome:请使用bing搜索;用gmail同步很香;

#### 科学的看世界
-  我选择的是shadowsocks-libev(因为我qt5以及普通的pip安装的shadowsocks就没有成功过)
    <pre><code> mkdir shadowsocks
    cd shadowsocks
    touch shadowsocks.json
    vim shadowsocks.json
    </code></pre>
-   将下面的内容根据自己的配置放进去:
    <pre><code>
    {
      "server":"my_server_ip",
      "server_port":53450,
      "local_address": "127.0.0.1",
      "local_port":1080,
      "password":"密码",
      "timeout":300,
      "method":"aes-256-gcm",
      "fast_open": false
    }
    </code></pre>
-   然后: ss-local -c ~/shadowsocks/shadowsocks/json & 
    自己测试一下有没有问题;
-   感谢阿姨的提醒,我决定用别名+脚本来启动shadowsocks(因为每次开机输入上面的东西实在没有效率)：
    -   先写一个自启动脚本：
    <pre><code> touch ~/.ssstart.sh
     vim ~/.ssstart.sh
    </code></pre>
    内容是:
    <pre><code>#!/bin/bash
    ss-local -c ~/shadowsocks/shadowsocks.json 
    </code></pre>
    -   然后在终端里面起别名:
    <pre><code>vim ~/.bashrc
    在末尾添加:
    alias ss='. ~/.ssstart.sh'
    :wq 保存,退出
    在终端里面: 
    source ~/.bashrc
    (如果是zsh:source ~/.zshrc)
    </code></pre>
    尝试一下在终端输入ss,它lei了;

#### 优化美化
-   官网安装网易云
-   官网安装vscode
-   配置zsh,tmux,vim:

##### zsh安装与美化
-   学习了:https://www.sysgeek.cn/install-zsh-shell-ubuntu-18-04/ 
https://segmentfault.com/a/1190000013612471 这两篇教程;
-   感谢何伟的配置文件;
-   相应的setting请参考我的github[相关内容](https://github.com/larryytr/Note_for_blog/tree/master/ubuntu).
-   安装zsh:
    <pre><code>sudo apt-get update
	sudo apt-get install zsh
	chsh -s /bin/zsh (设置zsh为默认)
    </code></pre>
-   重启你的ubuntu
-   安装oh-my-zsh插件:
    <pre><code> wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh
    </code></pre>
- 不改theme一无所有
- 准备使用powerline主题  
-   首先安装powerline字体：
    <pre><code>
    git clone https://github.com/powerline/fonts.git --depth=1
    # install
    cd fonts
    ./install.sh
    # clean-up a bit
    cd ..
    rm -rf fonts
    </code></pre>
- 安装完字体之后要记得使用：终端-编辑-首选项-文本-文本外观-自定义字体打勾-选一个带有powerline的。(星际玩家找了好久)
-   安装powerline: sudo apt install powerline 
-   我的配置见[相关内容](https://github.com/larryytr/Note_for_blog/tree/master/ubuntu)的setting .zshrc
-   颜色选择困难请: <pre><code>for code ({000..255}) print -P -- "$code: %F{$code}This is how your text would look like%f"</code></pre>
-   改完请source ~/.zshrc

##### tmux
-   tmux是一个很优秀的分屏软件,介绍可以看jyy的PA讲义以及自己搜索教程;
-   我使用了何伟的配置,具体见[相关内容](https://github.com/larryytr/Note_for_blog/tree/master/ubuntu)的setting

##### vim的美化
-   使用啦懒人vim: spf13-vim美化
-   请看[相关内容](https://github.com/larryytr/Note_for_blog/tree/master/ubuntu)的setting，找到并且下载spf13-vim.sh,然后bash spf13-vim.sh
-   我的配置同样在[相关内容](https://github.com/larryytr/Note_for_blog/tree/master/ubuntu)的setting里面;
-   这个时候的vim没有办法和系统剪切版交互,我根据https://www.cnblogs.com/memory4young/p/could-not-use-system-clipboard-in-vim.html 下载了其他一些插件:
    <pre><code>sudo apt-get install vim-scripts vim-gtk vim-gnome</pre></code>
    这样 vim --version|grep "cliboard" 会看到 +clipboard;
    然后就可以用+y,+p实现系统剪切版和vim剪切版的交互啦！

#### 其他内容:
- OSlab还需要:
  - sudo apt-get install curl
  - sudo apt-get install gcc-multilib
- git 配置请搜索廖雪峰

#### To be continued








