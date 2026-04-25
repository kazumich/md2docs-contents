---
title: "ディレクトリの並べ方"
date: "2026-04-04 09:00:00"
author: "appleple"
category: "guide/basics"
tags: ["authoring", "structure"]
order: 1
description: "contents/ 配下でディレクトリをどう切るか。セクションとサブセクションの整理方法。"
---

md2docs の `contents/` は**任意の階層**をサポートしています。ディレクトリの切り方 = サイトの構造そのものです。

## フラットに書くか、階層化するか

小さな docs（記事数 20 本以下くらい）なら、トップレベルのセクションに平置きする **フラット構成** が最もシンプルです。

```
contents/
├── getting-started/
│   ├── introduction.md
│   └── installation.md
└── guide/
    ├── writing-articles.md
    └── customization.md
```

記事が増えて特定セクションがごちゃついてきたら、**サブディレクトリで章立て** します。

```
contents/
└── guide/
    ├── writing-articles.md
    ├── basics/
    │   ├── directory-layout.md   ← このページ
    │   └── url-design.md
    └── advanced/
        └── customization.md
```

## サブディレクトリの扱い

- URL はそのままディレクトリ階層になります: `/guide/basics/directory-layout.html`
- 左サイドバーにはサブディレクトリのラベルが表示され、その配下の記事が一覧されます
- サブディレクトリのラベルを日本語にしたい場合は `config/categories.yaml` に定義を書きます

```yaml
categories:
  guide:
    label: "ガイド"
    categories:
      basics:
        label: "基本"
      advanced:
        label: "応用"
```

## おすすめの切り方

> [!TIP]
> 「章」のような単位で切ると、後から記事を追加しやすくなります。トピック単位（特定機能の深掘りなど）はサブディレクトリに分けず、1 本の記事で完結させる方がユーザーが探しやすいことが多いです。

- **セクション** (`contents/guide/`) = 読者の目的別の大分類
- **サブセクション** (`contents/guide/basics/`) = セクション内で 5 本以上になったら切る
- **さらに深い階層** (`contents/guide/basics/advanced/`) = 可能だが、基本は 2 階層までに留めた方が迷いません
