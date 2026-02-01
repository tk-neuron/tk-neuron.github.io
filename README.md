# Personal Site — Takuma Furukawa

個人の技術ブログ。noteから移行中。

## 概要

Jekyll + GitHub Pagesで構築した個人サイト。Markdown形式で記事を管理し、長期的なアーカイブを目指す。

## 技術スタック

- **Jekyll** 4.x — 静的サイトジェネレーター
- **GitHub Pages** — ホスティング
- **Markdown** — コンテンツ記述
- **SCSS** — スタイリング

## ローカル開発

### セットアップ

```bash
# 依存関係のインストール
bundle install

# ローカルサーバー起動
bundle exec jekyll serve

# ブラウザで確認
open http://localhost:4000
```

### ファイル構成

```
.
├── _config.yml          # サイト設定
├── _layouts/            # HTMLレイアウト
├── _posts/              # ブログ記事
├── assets/              # CSS, JS, 画像
│   └── main.scss
├── about.md
├── now.md
├── projects/
├── writing.md
└── colophon.md
```

## 運用フロー

1. **編集** — ローカルでMarkdownを書く
2. **Push** — Gitでバージョン管理
3. **公開** — GitHub Pagesが自動デプロイ

## note移行戦略

### 移行方針
- 重要な記事から順次移行
- Markdown形式に変換
- 画像などのアセットも自己管理

### 記事の構造

```markdown
---
layout: post
title: "記事タイトル"
date: YYYY-MM-DD
tags: [tag1, tag2]
---

## 概要
...

## 本文
...
```

## デザイン

### コンセプト
エディトリアルミニマリズム — 読みやすさと構造を重視。

### タイポグラフィ
- **見出し**: EB Garamond, Crimson Pro
- **本文**: Zen Kaku Gothic New
- **コード**: DM Mono

### CSS変数

```scss
:root {
  --ink: #1a1614;
  --accent: #5c4e3d;
  --step-0: clamp(1rem, 0.96rem + 0.2vw, 1.125rem);
}
```

## ライセンス

© 2026 Takuma Furukawa. All rights reserved.

---

*継続的に改善中。*

