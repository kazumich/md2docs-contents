---
title: "categories.yaml リファレンス"
date: "2026-04-03 10:00:00"
author: "appleple"
category: "reference"
tags: ["config", "reference"]
order: 2
description: "サイドバーのセクション定義 config/categories.yaml のキー一覧。"
---

左サイドバーに表示するセクションは `config/categories.yaml` で定義します。ここに書いていないセクションはナビに現れません（記事ファイル自体はあっても URL でアクセス可能ですが一覧は出ません）。

## 形式

```yaml
categories:
  {section-slug}:
    label: "表示名"
    description: "セクションの説明（任意）"
```

`{section-slug}` は URL の第 1 階層、および `contents/{section-slug}/` のディレクトリ名になります。

## 各キーの仕様

| キー | 型 | 必須 | 説明 |
|------|-----|-----|------|
| `label` | string | ✅ | ヘッダやサイドバーに表示される名前 |
| `description` | string | ❌ | セクション一覧ページのリード文に使用 |

## 設定例

```yaml
categories:
  getting-started:
    label: "はじめに"
    description: "md2docs の概要とセットアップ手順。"
  guide:
    label: "ガイド"
    description: "日々の運用で使う機能と記事執筆のガイド。"
  reference:
    label: "リファレンス"
    description: "設定・テンプレート変数・CLI コマンドの詳細リファレンス。"
```

## サイドバーの並び順

サイドバーに表示されるセクションの順序は、この YAML の**記載順**です。アルファベット順にはなりません。

> [!TIP]
> 新しいセクションを追加する場合、YAML を編集してから `contents/{新セクション}/` ディレクトリを作り、Markdown ファイルを置きます。サイドバーには次のリクエストから反映されます。

## 記事内の並び順は order で

セクション内の記事の並び順は `categories.yaml` では制御しません。各記事の front matter の `order` フィールドで指定します。詳細は [Front Matter リファレンス](/guide/front-matter.html) を参照してください。
