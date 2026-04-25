---
title: "URL 設計"
date: "2026-04-04 10:00:00"
author: "appleple"
category: "guide/basics"
tags: ["url", "structure"]
order: 2
description: "contents/ のディレクトリ構造が URL にどう反映されるか。"
---

URL は `contents/` 配下のファイルパスに一対一で対応します。ルールは単純です。

## ルール

| ファイル | URL |
|---------|-----|
| `contents/getting-started/introduction.md` | `/getting-started/introduction.html` |
| `contents/guide/basics/url-design.md` | `/guide/basics/url-design.html` |
| `contents/guide/basics/deep/topic.md` | `/guide/basics/deep/topic.html` |

## ディレクトリ一覧ページ

ディレクトリ自体もアクセスできます。その場合は直下の `.md` を一覧表示します。

| URL | 表示内容 |
|-----|---------|
| `/` | トップ（セクションカード） |
| `/guide` | `contents/guide/*.md` の一覧 |
| `/guide/basics` | `contents/guide/basics/*.md` の一覧 |

## スラッグ命名の指針

> [!IMPORTANT]
> URL は一度公開したら変えない前提で命名しましょう。外部からのリンクや SEO に影響します。

- **小文字 + ハイフン区切り**: `url-design.md` ✓、`UrlDesign.md` ✗
- **ASCII のみ**: 日本語スラッグは URL エンコードされ、コピペ時に冗長になるため非推奨
- **短く具体的に**: `writing.md` より `writing-articles.md` の方が後で探しやすい
