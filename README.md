# 株帳 PWA — iPhoneアプリ化の手順

## 1. GitHub Pagesで公開する(5分・無料)
PWAはHTTPSでの公開が必要です。最も簡単なのはGitHub Pagesです。

```bash
# Claude Codeやターミナルから
gh repo create kabucho --public
cd kabucho-pwa
git init && git add . && git commit -m "kabucho v1"
git branch -M main
git remote add origin https://github.com/<あなたのID>/kabucho.git
git push -u origin main
gh api repos/<あなたのID>/kabucho/pages -X POST -f "source[branch]=main" -f "source[path]=/"
```
またはGitHubのリポジトリ画面 → Settings → Pages → Branch: main で有効化。
数分後に `https://<あなたのID>.github.io/kabucho/` で公開されます。

※ 実データを入れるのは「ホーム画面に追加した後」です。公開されるのは
サンプルデータ入りのアプリ本体だけで、入力データは端末外に出ません。
非公開にしたい場合はprivateリポジトリ+Cloudflare Pages等でも可。

## 2. iPhoneにインストール
1. SafariでURLを開く
2. 共有ボタン(□↑) → 「ホーム画面に追加」
3. ホーム画面の「株帳」アイコンから起動 → 全画面のアプリとして動作

## 3. 特徴
- データは端末のlocalStorageに自動保存(サーバー送信なし)
- オフラインでも起動可能(Service Workerキャッシュ)
- 機種変更時は「帳簿を書き出す」→ 新端末で「読み込む」

## ファイル構成
- index.html … アプリ本体
- manifest.json … アプリ名・アイコン定義
- sw.js … オフラインキャッシュ
- icon-192.png / icon-512.png / apple-touch-icon.png … アイコン
