---
title: "カスタマイズ"
date: "2026-04-02 12:00:00"
author: "appleple"
category: "guide"
tags: ["customization", "theme"]
order: 4
description: "テーマ、ロゴ、カラー、Prism 対応言語などの変更方法。"
---

md2docs のテンプレート・アセット・見た目はすべてリポジトリ内で完結しています。必要に応じて好きに書き換えてください。

## テーマを切り替える

テンプレートセットは `themes/` 配下に置かれています。標準で 2 つ同梱しています。

| テーマ | 用途 |
|--------|------|
| `docs` | ドキュメントサイト向け（本サイト） |
| `default` | ブログ風レイアウト |

使うテーマは `config/site.yaml` で切り替えます。

```yaml
site:
  theme: "docs"
```

## カラーの変更

アクセントカラーは Tailwind のユーティリティクラスで統一しています。置換のポイントはだいたい次の 3 箇所です。

- `themes/docs/layout.html.twig` — ヘッダのロゴ色 (`text-sky-500`)
- `themes/docs/modules/nav_sidebar.html.twig` — アクティブなリンク (`text-sky-600`, `bg-sky-50`)
- `public/assets/docs/css/custom.css` — `.nav-link.active` と `.toc-link.active`

> [!TIP]
> プロジェクトで決まっているブランドカラーがある場合、先に Tailwind の theme 拡張で変数化してしまうと、後から一箇所で変更できるようになって便利です。

## ロゴ

ヘッダのロゴは `themes/docs/layout.html.twig` の SVG を直接書き換えます。SVG は `<header>` セクション内、`class="flex items-center gap-2 font-bold text-xl"` のリンクの中にあります。

画像にしたい場合は次のように差し替えます。

```html
<a href="/" class="flex items-center gap-2 font-bold text-xl text-slate-900">
  <img src="/assets/images/logo.svg" alt="{{ site.name }}" class="h-7 w-auto">
  {{ site.name }}
</a>
```

## Prism の対応言語を増やす

初期状態では HTML / CSS / JS / PHP / bash / YAML / JSON に対応しています。増やす場合は `themes/docs/layout.html.twig` の `<head>` に追加します。

```html
<script src="https://cdn.jsdelivr.net/npm/prismjs@1.29.0/components/prism-ruby.min.js"></script>
```

利用可能なコンポーネント一覧は [prismjs.com](https://prismjs.com/#languages-list) を参照してください。

## フッタ

フッタは `themes/docs/layout.html.twig` の最下部にあります。プライバシーポリシー等のリンクを追加する場合はここを編集してください。

> [!NOTE]
> 深いカスタマイズをする場合は、`themes/docs/` をまるごとコピーして `themes/your-theme/` を作り、`site.yaml` の `theme` を切り替えるのが安全です。upstream を追従する際の衝突が減ります。
