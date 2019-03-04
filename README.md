## Ubuntu 16.04LTS Config

#### Delete Amazon link

```bash
sudo apt remove unity-webapps-common
```



#### Change ubuntu source to tuna

```bash
sudo nano /etc/apt/sources.list
```

Replace all contains to follows

```bash
# tuna

deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-security main restricted universe multiverse
```

```bash
sudo apt update && sudo apt upgrade && sudo apt dist-upgrade
sudo apt autoremove
```



#### Change terminal appearance

Right-click terminal

`Profiles > Profile Preferance`

> Colors > Built-in schemes > White on black
>
> Colors > Use transparent background



#### Shadowsocks

install shadowsocks-libev from PPA

```bash
sudo apt-get install software-properties-common -y
sudo add-apt-repository ppa:max-c-lv/shadowsocks-libev -y
sudo apt-get update
sudo apt install shadowsocks-libev
```

install libsodium for `chacha20-ietf-poly1305` method

```bash
wget https://download.libsodium.org/libsodium/releases/libsodium-1.0.17.tar.gz
tar zxvf libsodium-1.0.17.tar.gz
cd libsodium-1.0.17
./configure
make && make check
make install
ldconfig
```

configure shadowsocks-libev

```bash
sudo nano /etc/shadowsocks-libev/config.json
```

```bash
{
    "server":"server_ip_address",
    "server_port":server_port,
    "local_address": "127.0.0.1",
    "local_port":1080,
    "password":"password",
    "timeout":300,
    "method":"chacha20-ietf-poly1305",
    "fast_open": true
}

```

open local shadowsocks service

```bash
sudo ss-local -c /etc/shadowsocks-libev/config.json
```

configure system proxy in `System Settings > Network > Network proxy`

> Method > Manual > Socks Host
>
> 127.0.0.1      1080



#### Chrome

```bash
sudo dpkg -i google-chrome-stable_current_amd64.deb 
```



#### VSCode

```bash
sudo dpkg -i code_1.31.1-1549938243_amd64.deb
```



#### Change theme

install unity-tweak-tool

```bash
sudo apt install unity-tweak-tool 
```

install Flatabulous theme

```bash
sudo add-apt-repository ppa:noobslab/themes
sudo apt update
sudo apt install flatabulous-theme
```

install Ultra-Flat icon

```bash
sudo add-apt-repository ppa:noobslab/icons
sudo apt update
sudo apt install ultra-flat-icons
```

configure theme and icon in unity-tweak-tool



#### Sogou input method

add sogou icon in Flatabulous theme

```bash
sudo cp fcitx-sogoupinyin.svg /usr/share/icons/Ultra-Flat/apps/scalable
```

install `fcitx`

```bash
sudo apt install fcitx
sudo apt install fcitx-config-gtk
```

`System Settings > Language Support`

>  change `keyboard input method system` to `fcitx`

```bash
sudo dpkg -i sogoupinyin_2.2.0.0108_amd64.deb 
sudo apt install -f
```

add sogou input method in `fcitx` settings (keyboard icon on the right top)

log out once

```bash
sudo service lightdm restart
```

configure shortcut for triggering input method

`Fcitx Settings > Global Config`

> Trigger Input Method > Super + Space

`System Settings > Text Entry`

> Super + Space -> Ctrl + Space
>
> Shift + Super + Space -> Shift + Ctrl + Space



#### Change screen shot shortcut

`System Settings > Keyboard > Shortcuts > Screenshots`

> Take a screenshot > Super + print



#### Install Git

```bash
sudo apt install git
```

Configure Git

```bash
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
git config --list
```

Generating a new SSH key

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Adding your SSH key to the ssh-agent

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```

Add the SSH key to your GitHub account

```bash
# Downloads and installs xclip. If you don't have `apt-get`, you might need to use another installer (like `yum`)
sudo apt-get install xclip

# Copies the contents of the id_rsa.pub file to your clipboard
xclip -sel clip < ~/.ssh/id_rsa.pub
```

paste your SSH key to Github



#### Install CMake

```bash
sudo apt install cmake
```



#### Install Typora

```bash
# or run:
# sudo apt-key adv --keyserver keyserver.ubuntu.com--recv-keys BA300B7755AFCFAE
wget -qO - https://typora.io/linux/public-key.asc | sudo apt-key add -

# add Typora's repository
sudo add-apt-repository 'deb https://typora.io/linux ./'
sudo apt-get update

# install typora
sudo apt-get install typora
```



#### Install WPS

uninstall LibreOffice

```bash
sudo apt remove libreoffice-common
```

install WPS from .deb file

```bash
sudo dpkg -i wps-office_10.1.0.6757_amd64.deb
```

add lacking fonts files

```bash
sudo mv wps_symbol_fonts /usr/share/fonts/
```

reboot