---
title: ZSH 配置與好用的工具
categories: Linux
tags: linux
---
先前的文章有介紹如何在`Windows WSL` 內安裝`Oh My Zsh` 與`Powerlevel10k`，
還沒設定的請移步到[Windows Terminal 搭配WSL](https://shoudevops.github.io/Windows/wsl-terminal/)

這裡會再延伸說明`Oh My Zsh` 下有什麼方便好用的工具

## ZSH-Autosuggestions

* 參考[官方文件](https://github.com/zsh-users/zsh-autosuggestions)

* Clone this repository into $ZSH_CUSTOM/plugins (by default ~/.oh-my-zsh/custom/plugins)

```shell
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

* Add the plugin to the list of plugins for Oh My Zsh to load (inside ~/.zshrc):

```.zshrc
plugins=( 
    # other plugins...
    zsh-autosuggestions
)
```

* Refresh ~/.zshrc

```shell
source ~/.zshrc
```

## ZSH-Syntax-Highlighting

* 參考[官方文件](https://github.com/zsh-users/zsh-syntax-highlighting)

* Clone this repository in oh-my-zsh's plugins directory:

```shell
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

* Activate the plugin in ~/.zshrc:

```.zshrc
plugins=( [plugins...] zsh-syntax-highlighting)
```

* Refresh ~/.zshrc

```shell
source ~/.zshrc
```

## ZSH-Completions

* 參考[官方文件](https://github.com/zsh-users/zsh-completions)

* Clone the repository inside your oh-my-zsh repo:

```shell
  git clone https://github.com/zsh-users/zsh-completions ${ZSH_CUSTOM:=~/.oh-my-zsh/custom}/plugins/zsh-completions
```

* Enable it in your .zshrc by adding it to your plugin list and reloading the completion:

```./zshrc
plugins=(… zsh-completions)

# 加入到~/.zshrc 的最後一行
autoload -U compinit && compinit
```

* Refresh ~/.zshrc

```shell
source ~/.zshrc
```

## Linux Homebrew

* 參考[官方文件](https://brew.sh/)

* Install Homebrew

```shell
sudo apt install -y curl

/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> $HOME/.zshrc

eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"

sudo apt-get install build-essential

brew install gcc
```

## 其它工作需求工具

### Git

```shell
sudo apt-get update && sudo apt-get upgrade -y

sudo apt-get install git-core

git config --global user.name "$USER_NAME"

git config --global user.email "$USER_EMAIL"
```

### Docker Engine

* 參考[官方文件](https://docs.docker.com/engine/install/ubuntu/)

```shell
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker $USER_NAME
```

* Logout or Reboot

### Google Cloud SDK

* 參考[官方文件](https://cloud.google.com/sdk/docs/install)

```shell
echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list

sudo apt-get install apt-transport-https ca-certificates gnupg

curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add -

sudo apt-get update && sudo apt-get install google-cloud-sdk
```

### Kubectl

* 如果先裝好`Google Cloud SDK`

```shell
sudo apt-get install kubectl
```

### Kubectx

* 參考[官方文件](https://cloud.google.com/sdk/docs/install)

```shell
sudo git clone https://github.com/ahmetb/kubectx /opt/kubectx

sudo ln -s /opt/kubectx/kubectx /usr/local/bin/kubectx

sudo ln -s /opt/kubectx/kubens /usr/local/bin/kubens
```

* 套用到`Oh-My-Zsh` 的`zsh-completions`

```shell
mkdir -p ~/.oh-my-zsh/completions

chmod -R 755 ~/.oh-my-zsh/completions

ln -s /opt/kubectx/completion/kubectx.zsh ~/.oh-my-zsh/completions/_kubectx.zsh

ln -s /opt/kubectx/completion/kubens.zsh ~/.oh-my-zsh/completions/_kubens.zsh
```

* 如果已經設定好`zsh-completions`

```shell
source ~/.zshrc
```

### Nodejs

* 參考[官方文件](https://nodejs.org/zh-tw/download/package-manager/)

* Node.js v16.x:

```shell
# Using Ubuntu
curl -fsSL https://deb.nodesource.com/setup_16.x | sudo -E bash -

sudo apt-get install -y nodejs
```

* Node.js v14.x

```shell
# Using Ubuntu
curl -fsSL https://deb.nodesource.com/setup_14.x | sudo -E bash -

sudo apt-get install -y nodejs
```

* Node.js v12.x

```shell
# Using Ubuntu
curl -fsSL https://deb.nodesource.com/setup_12.x | sudo -E bash -

sudo apt-get install -y nodejs
```

* Node.js LTS

```shell
# Using Ubuntu
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt-get install -y nodejs
```

### Hexo

* 參考[官方文件](https://hexo.io/zh-tw/docs/)

* 如果已經安裝好Git, Node.js v12.x

```shell
npm install -g hexo-cli
```
