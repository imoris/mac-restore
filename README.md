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

# install yarn
$ brew yarn --ignore-dependencies
```

## アプリ再インストール / dotfilesリストア手順
``` bash
$ cd [where Brewfile is located]

# install necessary apps
$ brew bundle

# dotfilesのリストア
$ mackup restore
```

## 他実施事項
- app storeでbettersnaptoolをダウンロード＆インストール
- google日本語入力をダウンロード＆インストール
- karabinerのsimple modificationでApple Internal Keyboardに対してcaps_lockとleft_controlを入れ替え
- 設定 => Keyboard => Shortcutsでoption + spacebarでspotlight起動 
- 設定 => Mouse => Scroll Direction: Naturalのチェックを外す
- 設定 => Trackpad => Point&Click => secondary click (右下端をクリック）へ変更、Tap to Clickにチェックを入れる


 

