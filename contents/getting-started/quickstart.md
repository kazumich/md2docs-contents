---
title: "クイックスタート"
date: "2026-04-01 11:00:00"
author: "appleple"
category: "getting-started"
tags: ["intro", "tutorial"]
order: 3
description: "5 分で最初のページを公開するまでの手順。"
---

このページでは、新しい記事を 1 本書いてブラウザで確認するところまでを最短手順で説明します。[インストール](/getting-started/installation.html) が完了している前提です。

## 記事を 1 本書く

`contents/` 配下に好きなセクションを選び、Markdown ファイルを作成します。

```bash
mkdir -p contents/guide
$EDITOR contents/guide/hello.md
```

ファイルの中身はこんな感じです。

```markdown
---
title: "はじめての記事"
date: "2026-04-15 12:00:00"
author: "appleple"
category: "guide"
order: 1
description: "自分で書いた最初のページ。"
---

# はじめての記事

ここから本文を Markdown で書きます。

## 小見出し

段落、**強調**、`インラインコード`、リストなどが使えます。

- りんご
- みかん
- バナナ
```

## ブラウザで確認

開発サーバが起動していれば、次の URL で確認できます。

```
http://localhost:8080/guide/hello.html
```

左サイドバーの「ガイド」にも自動で追加されます。

> [!TIP]
> 並び順は front matter の `order` で制御します。`order: 1` が一番上、数字が大きいほど下へ。`order` が無い記事は日付の新しい順に並びます。

## 次の一歩

- 記事の書き方をもっと詳しく: [記事の書き方](/guide/writing-articles.html)
- Front Matter の全項目: [Front Matter リファレンス](/guide/front-matter.html)
- サイト全体の設定: [site.yaml リファレンス](/reference/site-config.html)
