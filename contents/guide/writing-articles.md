---
title: "記事の書き方"
date: "2026-04-02 09:00:00"
author: "appleple"
category: "guide"
tags: ["authoring", "markdown"]
order: 1
description: "Markdown と YAML フロントマターで記事を書くときのルール。"
---

md2docs の記事は、ヘッダに YAML フロントマター、本文に Markdown を書いた単一のファイルです。このページでは、執筆時に押さえておきたい書き方をまとめます。

## ファイルの基本構造

```markdown
---
title: "ページタイトル"
date: "2026-04-01 09:00:00"
author: "appleple"
category: "guide"
order: 1
description: "一覧や OGP に使う短い説明文。"
---

本文を Markdown で書きます。
```

ファイルは `contents/{section}/{slug}.md` に配置します。`section` が URL の第 1 階層、`slug` が第 2 階層になります。

## 見出しの階層

md2docs では次のルールで見出しを扱います。

- `h1` はページに 1 つ（本文の先頭見出し、通常はタイトルと一致）
- `h2` は右サイドバー目次のトップレベル
- `h3` は右サイドバー目次のネスト階層
- `h4` 以下は目次に入らない

> [!NOTE]
> 見出しの ID は自動で付与されます。日本語の見出しにはそのまま日本語のアンカーが生成されます。手動で ID を指定したい場合は、生 HTML でも書けます（ただし Markdown としての可読性は下がります）。

## コードブロック

コードフェンスに言語名を付けると、Prism.js がハイライトします。

~~~markdown
```php
<?php
echo 'Hello';
```
~~~

対応言語は初期状態で HTML、CSS、JavaScript、PHP、bash、YAML、JSON です。追加したい場合は [カスタマイズ](/guide/customization.html) を参照してください。

## 表

標準的な GFM (GitHub Flavored Markdown) の表が使えます。

| オプション | 型 | 必須 | 初期値 |
|-----------|------|-----|--------|
| `title` | string | ✅ | — |
| `date` | string | ✅ | — |
| `order` | int | ❌ | なし |

## 注意喚起（Callout）

重要な情報はコールアウトで強調できます。

```markdown
> [!NOTE]
> 補足情報。

> [!TIP]
> 便利な小ワザ。

> [!IMPORTANT]
> 必ず押さえておくべきこと。

> [!WARNING]
> 注意が必要な操作。

> [!CAUTION]
> 取り返しがつかない可能性がある操作。
```

詳しくは [Callout の使い方](/guide/callouts.html) を参照してください。

## 画像

画像は `public/assets/images/` 配下に置き、記事からは絶対パスで参照します。

```markdown
![スクリーンショット](/assets/images/screenshots/home.png)
```

> [!TIP]
> 画像も git で管理するため、バイナリが大きくならないように WebP や圧縮済み PNG を推奨します。

## 記事間のリンク

他の記事へのリンクは、`.md` でも `.html` でも、どちらで書いても構いません。サイト表示時には内部リンクの `.md` は自動的に `.html` に書き換えられます。

```markdown
詳細は [インストール](/getting-started/installation.md) を参照してください。
```

> [!TIP]
> `.md` で書いておくと、**GitHub 上で記事を直接閲覧した時にもリンクが追跡できる**、VS Code で Cmd+クリックしてファイルに飛べる、などの副次的メリットがあります。チームで Markdown を書くプロジェクトでは `.md` を推奨します。

例えば、[Front Matter リファレンス](/guide/front-matter.md) や [Callout の使い方](/guide/callouts.md) へのリンクもこの `.md` 記法で書けます。
