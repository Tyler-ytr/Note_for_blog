# ubuntu复活记
这是我今天第四次重装ubuntu,心情非常悲痛;
- 之前崩的原因是搜狗输入法安装的时候没有提前安装fcix框架,导致乱码然后系统就傻掉了;
- 重装很多次的原因是因为没有在重装之前完全的格式化分区,我建议每一次玩具坏了都要用windows格式化一次呜呜呜
- 下面是正式的复活操作:
- sudo passwd(修改sudo密码)
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





