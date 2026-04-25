# md2docs-contents

[md2docs](https://github.com/kazumich/md2docs) で公開しているドキュメントサイトのコンテンツリポジトリです。

このリポジトリには記事 Markdown とサイト構造定義しか入っていません。レンダリングは [md2docs](https://github.com/kazumich/md2docs) エンジン側に任せ、**執筆者はこのリポジトリだけ clone すれば十分**です。PHP も Composer も Node.js もインストール不要。

## クイックスタート（執筆者向け）

### 方法 A: GitHub Web UI で直接編集

1. リポジトリで該当の `.md` ファイルを開く
2. 鉛筆アイコン (✏️) で編集
3. ページ下部「Commit changes」でコミット
4. `main` への変更は数分で本番サイトに反映

軽い修正なら一番簡単。Markdown プレビューも GitHub 上で見られます。

### 方法 B: ローカルで編集

```bash
git clone https://github.com/kazumich/md2docs-contents.git
cd md2docs-contents
```

1. `contents/` 配下の Markdown を編集
2. 普通の git 操作でコミット → push
3. **`main` への push で自動デプロイ**（GitHub Actions が XSERVER に FTP）

## ディレクトリ構成

```
md2docs-contents/
├── contents/               # 記事本体 (Markdown)
│   ├── getting-started/
│   │   └── *.md
│   ├── guide/
│   │   ├── *.md
│   │   └── basics/         # サブカテゴリ可 (任意の深さ)
│   │       └── *.md
│   └── reference/
│       └── *.md
└── categories.yaml         # トップレベル & サブのラベル・並び順定義
```

URL は `contents/{セクション}/{ファイル名}.html` の形式でそのまま反映：

| ファイル | URL |
|---------|-----|
| `contents/guide/installation.md` | `/guide/installation.html` |
| `contents/guide/basics/setup.md` | `/guide/basics/setup.html` |

## 記事の書き方

ファイル先頭に YAML フロントマター、本文を Markdown で書きます。

```markdown
---
title: "ページタイトル"
date: "2026-04-25 12:00:00"
order: 1
description: "一覧やサイドバーで表示する説明文"
tags: ["intro", "setup"]
---

# 本文

普通の Markdown です。コードブロック、表、リスト、リンクが使えます。

## GitHub 風 callout

> [!NOTE]
> 補足情報（青）

> [!TIP]
> ヒント（緑）

> [!IMPORTANT]
> 重要（紫）

> [!WARNING]
> 注意（黄）

> [!CAUTION]
> 警告（赤）

## 記事間リンク

`.md` で書けば自動で `.html` に変換されます。

[インストール](/getting-started/installation.md) を参照してください。
```

執筆ルールの詳細は本番サイトの「ガイド」セクションを参照してください: <https://md2docs.a-blog.jp/guide/>

## さらに詳しい運用

ブランチ運用・PR レビュー・ローカルプレビュー・デプロイ設定などの詳細は、エンジン側のドキュメントを参照してください: [kazumich/md2docs](https://github.com/kazumich/md2docs)
