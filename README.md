# Macbook再インストール時設定手順

## 前準備
- 移行元Macでmackup実行
``` bash
$ mackup backup
```

- 移行先MacでのhomebrewおよびDropboxのinstall
``` bash
# install homebrew
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

# install dropbox
$ brew cask install dropbox
```

## アプリ再インストール / dotfilesリストア手順
``` bash
$ cd [where Brewfile is located]

# install necessary apps
$ brew bundle

# dotfilesのリストア
$ mackup restore
```


 

