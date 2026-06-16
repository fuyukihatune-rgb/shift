# Shift

DIDシステム向けの「今、誰がフロントにいるか」を管理し、アルター同士で申し送り（メッセージ）をするためのアプリ。
タイムライン形式で記録する兄弟アプリ **Mosaic** と対になる存在として設計されています。

- 静的サイト（HTML + JS + CSS、外部フレームワーク不使用）
- PWA 対応（ホーム画面追加・オフライン動作）
- データは `localStorage` のみ。サーバー不要・通信なし・完全プライベート

## ファイル構成

```
shift/
├── index.html     ← アプリ全体（HTML + CSS + JS を1ファイルに収める）
├── manifest.json  ← PWAマニフェスト
├── sw.js          ← Service Worker
└── icons/
    ├── icon-192.png  ← PWAアイコン（192×192px）※別途用意が必要
    └── icon-512.png  ← PWAアイコン（512×512px）※別途用意が必要
```

> **注意**: `manifest.json` と `index.html` は `icons/icon-192.png` / `icons/icon-512.png` を参照します。
> ホーム画面アイコンを表示するには、この2枚のPNGを `icons/` に配置してください（無くてもアプリ自体は動作します）。

## Cloudflare Pages での公開

1. GitHub に `shift` リポジトリを作成（Public）
2. `shift/` フォルダの中身をすべて push
3. Cloudflare Pages → 「新しいプロジェクトを作成」
4. GitHub リポジトリ `shift` を接続
5. ビルド設定
   - フレームワークプリセット: なし
   - ビルドコマンド: （空欄）
   - 出力ディレクトリ: `/`
6. 「保存してデプロイ」
7. デプロイ完了 → `shift.pages.dev` でアクセス確認
8. カスタムドメイン設定（例: `shift.xdcyw.net`）
   - Cloudflare Pages → カスタムドメイン → ドメイン追加
   - DNS に CNAME レコードを追加（Cloudflare が自動案内）

## ローカル確認

ブラウザで `index.html` を直接開くと Service Worker が動作しません。
ローカルで確認する場合は以下のいずれかを使います:

```sh
# Python
python3 -m http.server 8080

# Node.js
npx serve .
```

→ http://localhost:8080 でアクセス

---

© 田中志 / Ataraxia Works

## アップデート履歴

## 2026-06-16
- OGタグ追加（og:title / og:description / og:image / og:url / og:type / twitter:card）
- キーボードアクセシビリティ改善（:focus-visible スタイル追加）
- manifest.json 整備（scope・categories・orientation 修正）
