+++
title = 'WSL'
date = 2024-10-23T17:17:36+08:00
draft = false
tags = [ 'WSL' ]
categories = '开发工具'
+++

## 宿主机访问不到 `WSL` 内 `Docker` 的端口, 比如 3006 / 6379

关闭 `WSL` 防火墙:

```shell
ufw disable
```

<br>

## 间隔一段时间后, 第一个请求响应慢

关闭: `fastcgi_buffering`

```nginx
server {
    ...
    location ~ \.php$ {
        ...
        fastcgi_buffering off;
        ...
    }
}
```

修改 nginx 配置中 worker_connections 的值， 原来10240 改为65535，修改后重启。

```nginx
events {
  worker_connections 65535;
}
```

<br>

## `.wslconfig` 配置

该配置是 `WSL` 的全局配置 -> [官方文档](https://learn.microsoft.com/zh-cn/windows/wsl/wsl-config#wslconfig)

推荐配置:
```
[wsl2]
networkingMode=mirrored # 开启镜像网络
dnsTunneling=true # 开启 DNS Tunneling
firewall=false #  Windows 防火墙
autoProxy=true # 自动同步代理

[experimental]
hostAddressLoopback=true
```

## 常用软件 (Ubuntu)

### zsh

```shell
apt install zsh
```

### oh-my-zsh

#### 安装

```shell
# curl
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# wget
sh -c "$(wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

#### 主题: `powerlevel10k`

[项目地址](https://github.com/romkatv/powerlevel10k)

- 字体
    - [MesloLGS NF Regular.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Regular.ttf)
    - [MesloLGS NF Bold.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold.ttf)
    - [MesloLGS NF Italic.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Italic.ttf)
    - [MesloLGS NF Bold Italic.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold%20Italic.ttf)

```shell
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

执行 `source ~/.zshrc` 触发主题配置

#### 插件: `zsh-autosuggestions`

[项目地址](https://github.com/zsh-users/zsh-autosuggestions)

```shell
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

#### 插件: `zsh-syntax-highlighting`

[项目地址](https://github.com/zsh-users/zsh-syntax-highlighting)

```shell
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

#### 修改配置

```zsh
plugins=( git z zsh-syntax-highlighting zsh-autosuggestions)
```

### nvm

```shell
# curl
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash

# wget
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
```

### vim

[vimrc](http://slowlyo.top/index.php/archives/7/)

### eza

[项目地址](https://github.com/eza-community/eza)

```bash
sudo apt update
sudo apt install -y gpg

sudo mkdir -p /etc/apt/keyrings
wget -qO- https://raw.githubusercontent.com/eza-community/eza/main/deb.asc | sudo gpg --dearmor -o /etc/apt/keyrings/gierens.gpg
echo "deb [signed-by=/etc/apt/keyrings/gierens.gpg] http://deb.gierens.de stable main" | sudo tee /etc/apt/sources.list.d/gierens.list
sudo chmod 644 /etc/apt/keyrings/gierens.gpg /etc/apt/sources.list.d/gierens.list
sudo apt update
sudo apt install -y eza
```

#### 配置

```zsh
alias ls="eza --time-style '+%Y-%m-%d %H:%M' -g --icons=always"
alias ll="ls -la"
```
