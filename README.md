# Macbook再インストール時設定手順

## 注意事項
### 1. 背景と問題点
- Mackup は設定ファイルをクラウドストレージ（Dropbox/Google Drive/iCloudなど）に symlink で退避します。
- **Sequoia 以降**はセキュリティ強化により、  
  - DriverKit/アクセシビリティ経由のプロセス  
  - root 権限で動く補助プロセス  
  がクラウド配下の symlink を読めなくなるケースが多発。  
- 結果：**Karabiner / BetterSnapTool / BetterTouchTool / Zoom / Spotify / iTerm2 / VSCode / Cursor** などが設定を読み込めず挙動不良。

### 2. 運用方針
- **Mackupの保存先は必ずローカル**（例: `~/mackup_backup`）にする  
- クラウド（Google Drive 等）はあくまで **コピー置き場**  
- **権限が絡むアプリは Mackup から除外し、手動コピー**

### 3. `.mackup.cfg` 設定例
```ini
[storage]
engine = file_system
path = ~/mackup_backup

[applications_to_ignore]
karabiner-elements
bettersnaptool
bettertouchtool
zoom
spotify
vscode
cursor
iterm2
git
```

### 4. バックアップ手順（旧端末側）
```bash
mkdir -p ~/mackup_backup
mackup backup
cd ~
tar -czf mackup_backup_$(date +%Y%m%d).tar.gz mackup_backup
# Google Drive の実際のマウント先に移動
mv mackup_backup_*.tar.gz ~/Library/CloudStorage/GoogleDrive-<アカウント>/My\ Drive/backup/
```

### 5. 復元手順（新端末側）

```bash
# 1. Homebrew をインストール
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew install mackup

# 2. バックアップを展開
cd ~
tar -xzf mackup_backup_YYYYMMDD.tar.gz

# 3. ~/.mackup.cfg を編集し、保存先を ~/mackup_backup に合わせる
vi ~/.mackup.cfg

# 4. 復元
mackup restore
```

### 6. 安全性チェック
- Terminal に Full Disk Access を付与してから実行
```bash
while IFS= read -r l; do
  tgt=$(readlink "$l")
  case "$tgt" in
    *"/CloudStorage/"*|*"/Google Drive/"*|*"/GoogleDrive-"*|*"/Dropbox/"*|*"/OneDrive/"*|*"/Documents/mackup_"* )
      printf '[RISK] %s -> %s\\n' "$l" "$tgt";;
  esac
done <<EOF
$(find "$HOME/Library/Preferences" "$HOME/Library/Application Support" "$HOME/.config" -type l 2>/dev/null)
EOF
```

### 7. 再承認が必要な権限例
- BetterTouchTool / BetterSnapTool / Karabiner → アクセシビリティ
- Zoom → 画面収録・マイク・カメラ

### 8. よくある注意点
- JSON の lint は jq を使用（plutil は plist 用）
- iTerm2 DynamicProfiles は ~/Library/Application Support/iTerm2/DynamicProfiles に置く
- Brewアプリは brew bundle dump --file=~/Brewfile で管理し、復元は brew bundle --file=~/Brewfile

### 9. 推奨ワークフロー
- 旧Macで mackup backup → ローカル保存
- ~/mackup_backup を tar.gz に固めてクラウドへ
- 新Macで展開 → mackup restore
- 除外アプリは手動コピー
- RISKチェックで symbolic link が残っていないことを確認
- 各アプリを再起動 & 権限を再承認

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




 

