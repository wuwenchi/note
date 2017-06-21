### 1、禁止光标闪烁
```
gsettings set org.gnome.desktop.interface cursor-blink false
```

### 2、添加gcc编译工具
```
vim ~/.bashrc
```
在最后末尾输入
```
export PATH=$PATH:/home/wuwenchi/tool/gcc-arm-none-eabi-4_9-2015q3/bin
```
之后退出编辑，在终端输入：
```
source ~/.bashrc
```
之后可以使用 arm tab tab 来看是否加入成功

### 3、卸载modemmanage
```
sudo apt --purge remove modemmanager
```

### 4、添加用到到工作组
```
sudo usermod -a -G dialout $USER
```

### 5、常用的软件
```
vim gawk python-empy git genromfs ctags cscope minicom silversearcher-ag vim-gnome lib32bz2-dev lib32gcc1 shutter unity-tweak-tool
```

```
sudo apt-get install compizconfig-settings-manager compiz-plugins
```
主题设置软件




### 6、常识
##### 搜索更新列表
`sudo apt-cache search`

##### 查看已经安装的文件
`dpkg --list`

##### 添加root密码
`sudo passwd root`

##### 解决python的串口依赖库问题
```
sudo apt install python-setuptools
sudo easy_install pyserial
```
### 7、主题和图标
```
sudo add-apt-repository ppa:noobslab/themes
sudo add-apt-repository ppa:noobslab/icons
sudo apt-get update
sudo apt-get install ultra-flat-icons
sudo apt-get install arc-theme
```

### 8、配置cscope
```
find . \( -path "./AntennaTracker" -o -path "./APMrover2" -o -path "./ArduPlane" \) -prune -o  -name "*.cpp" -o -name "*.c" -o -name "*.h" > cscope.files
cscope -Rbkq -i cscope.files
```
更新cscope数据库之后，需要在vim里面更新链接文件：

`cscope reset`

### 9、不能正常更新
```
sudo rm /var/lib/apt/lists/* -vfR
sudo apt update
```

### 10、安装 VMware
```
chmod a+x VMware-Workstation-Full-11.0.0-2305329.x86_64.bundle
sudo ./VMware-Workstation-Full-11.0.0-2305329.x86_64.bundle
```
序列号：5A02H-AU243-TZJ49-GTC7K-3C61N

### 11、terminal快捷键


| Ctrl+         | 作用       |
| ------------- | -------- |
| a             | 行首       |
| e             | 行尾       |
| f             | 光标右移     |
| b### 1、禁止光标闪烁 | 光标左移     |
| h             | 删除左边字符   |
| d             | 删除当前字符   |
| w             | 删除左边一个单词 |
| u             | 清除光标至行首  |
| k             | 清除光标至行尾  |
| l             | 清屏       |

### 12、安装星际译王
1、先安装软件：
```
sudo apt-get install stardict
```
2、然后去网站： http://abloz.com/huzheng/stardict-dic/zh_CN/ 下载朗道英汉字典
3、最后把解压后的文件夹放到词典目录
```
sudo mv stardict-kdic-computer-gb-2.4.2 /usr/share/stardict/dic/.
```

### 13、给64位系统添加32位软件库支持
```
sudo dpkg --add-architecture i386 
sudo apt-get update 
sudo apt install lib32z1
```
### 14、更改 CapsLock 按键

```
vim ~/.Xmodmap
```
1)、CapsLock 和 Ctrl 互换：
```
remove Lock = Caps_Lock
remove Control = Control_L
keysym Control_L = Caps_Lock
keysym Caps_Lock = Control_L
add Lock = Caps_Lock
add Control = Control_L
```
2)、CapsLock 改为 Ctrl：
```
remove Lock = Caps_Lock
remove Control = Control_R
keysym Control_R = Caps_Lock
keysym Caps_Lock = Control_R
add Lock = Caps_Lock
add Control = Control_R
```
window 上使用 mapkeyboard

### 15、安装便笺和查看系统信息指示

```
sudo add-apt-repository ppa:umang/indicator-stickynotes
sudo apt-get update
sudo apt-get install indicator-stickynotes
sudo apt-get install indicator-multiload
```
### 16、主题图标

```
sudo add-apt-repository ppa:noobslab/themes
sudo add-apt-repository ppa:noobslab/icons
sudo apt-get update
sudo apt-get install ultra-flat-icons
sudo apt-get install arc-theme
```