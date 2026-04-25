---
title: "ディレクトリ構成"
date: "2026-04-03 11:00:00"
author: "appleple"
category: "reference"
tags: ["reference", "architecture"]
order: 3
description: "md2docs のリポジトリに含まれるディレクトリと責務の一覧。"
---

md2docs は責務ごとにディレクトリを分けた、小さな PHP プロジェクトです。

## トップレベル

```
md2docs/
├── bin/          # CLI スクリプト
├── config/       # サイト設定
├── contents/     # 記事本体（Markdown）
├── document/     # 内部仕様書
├── public/       # Web 公開ディレクトリ（DocumentRoot）
├── src/          # PHP アプリケーションコード（PSR-4: Md2Docs\）
├── themes/       # Twig テンプレート
├── var/          # キャッシュ（git 管理外）
├── vendor/       # Composer 依存（git 管理外）
├── composer.json
├── package.json
├── LICENSE
└── README.md
```

## `src/` の中身

| ディレクトリ | 名前空間 | 責務 |
|-------------|----------|------|
| `src/Core/` | `Md2Docs\Core` | Application（ブート・ルーティング）、Router、Request、Config |
| `src/Model/` | `Md2Docs\Model` | Entry、Category などのドメインモデル |
| `src/Repository/` | `Md2Docs\Repository` | EntryRepository、CategoryRepository、TagIndexRepository |
| `src/Support/` | `Md2Docs\Support` | HtmlPostProcessor 等の補助処理 |

## `themes/` の中身

```
themes/
├── default/      # ブログ風テーマ（旧 a-column 由来）
│   ├── layout.html.twig
│   ├── home.html.twig
│   ├── entry.html.twig
│   ├── category.html.twig
│   ├── tag.html.twig
│   ├── 404.html.twig
│   └── modules/
└── docs/         # ドキュメントサイト用テーマ（本サイト）
    ├── layout.html.twig
    ├── home.html.twig
    ├── entry.html.twig
    ├── category.html.twig
    ├── tag.html.twig
    ├── search.html.twig
    ├── 404.html.twig
    └── modules/
        ├── nav_sidebar.html.twig
        └── toc.html.twig
```

## `public/` の中身

```
public/
├── index.php      # フロントコントローラ
├── .htaccess      # Apache URL 書き換え
└── assets/
    └── docs/
        ├── css/custom.css
        └── js/app.js
```

## `var/` の中身（git 管理外）

| パス | 内容 |
|------|------|
| `var/cache/twig/` | Twig コンパイル済みテンプレート |
| `var/cache/tags/` | タグインデックス JSON（自動再生成） |
| `var/fts.sqlite` | 全文検索インデックス（フェーズ 4 で導入予定） |

> [!NOTE]
> `var/` 以下はキャッシュのため、削除して問題ありません。次回リクエスト時に再生成されます。

## 外部への出入り

| パス | 扱い |
|------|------|
| `contents/` | **git 管理**: 記事。Pull Request のレビュー対象 |
| `themes/` | **git 管理**: テンプレート。UI 変更のレビュー対象 |
| `config/` | **git 管理**: サイト設定 |
| `.env` | git 管理外（`.gitignore`） |
| `vendor/` | git 管理外、`composer install` で再生成 |
| `var/` | git 管理外、ランタイムで再生成 |
