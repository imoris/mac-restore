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
- karabiner-elementsのsimple modificationでApple Internal Keyboardに対してcaps_lockとleft_controlを入れ替え
- karabiner-elementsのFunction KeysでUse all F1, F2, etc. keys as standard function keysにチェックを入れる
- 設定 => Keyboard => Shortcutsでoption + spacebarでspotlight起動
- 設定 => Keyboard => Shortcuts => Input SourcesでSelect the previous input sourceのチェックを外す
- 設定 => Keyboard => Input Source でU.S.およびHiragana(Google)以外の入力方法を削除する
- 設定 => Mouse => Scroll Direction: Naturalのチェックを外す
- 設定 => Trackpad => Point&Click => secondary click (右下端をクリック）へ変更、Tap to Clickにチェックを入れる
- 設定 => Bluetooth => Show Bluetooth in menu barにチェックを入れる

## Parallels関連
- [WindowsのGoogle日本語入力をIME offとIME onを割り当てる](https://www.teradas.net/archives/2927/)  
 => Karabinarの設定次第だが、自分の場合仮想winで左commandキー単体押しでCtrl+Shift+F11、右コマンドキー単体押しでCtrl+Shift+F12を割り当てており、それぞれをIME off、IME onにキーバインド設定をGoogle日本語入力で設定する
  - 入力文字なし(precompostion) ：Ctrl+Shift+F11 → IMEを無効化
  - 入力文字なし（precompostion) ：Ctrl+Shift+F12 → ひらがなに入力切替
  - 直接入力 (Direct Input) ：Ctrl+Shift+F12 → ひらがなに入力切替
  - 変換前入力中 (compostion)：Ctrl+Shift+F12 → ひらがなに入力切替
- [Parallels Desktopでリモートデスクトップ接続を利用した際にShiftキーが利用出来なくなる問題の解消方法](https://webnetforce.net/parallels-desktop-not-work-shift-key/)
- [Windowsのリモートデスクトップの接続が遅い時の対処方法](https://engineer-world.duckdns.org/2016/08/26/post-457/)




 

