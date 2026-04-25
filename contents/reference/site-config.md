---
title: "site.yaml リファレンス"
date: "2026-04-03 09:00:00"
author: "appleple"
category: "reference"
tags: ["config", "reference"]
order: 1
description: "config/site.yaml のキー一覧と初期値。"
---

サイト全体の設定は `config/site.yaml` に書きます。全てのキーは `site:` 配下にネストします。

## 基本情報

| キー | 型 | 初期値 | 説明 |
|------|-----|--------|------|
| `site.name` | string | `"md2docs"` | サイト名。`<title>` やヘッダのロゴで使用 |
| `site.description` | string | `""` | サイト説明文。OGP の description に使用 |
| `site.url` | string | `""` | 公開 URL（末尾スラッシュなし）。OGP `og:url` に使用 |
| `site.timezone` | string | `"Asia/Tokyo"` | PHP のタイムゾーン |

## 表示設定

| キー | 型 | 初期値 | 説明 |
|------|-----|--------|------|
| `site.theme` | string | `"docs"` | `themes/` 配下のテーマ名 |
| `site.entries_per_page` | int | `10` | セクション一覧の 1 ページあたり件数 |
| `site.home_entries_per_category` | int | `5` | トップのセクション別最新件数 |
| `site.excerpt_length` | int | `200` | 抜粋の最大文字数 |
| `site.date_format` | string | `"Y/m/d"` | 一覧の日付フォーマット |
| `site.tag_cloud_min_count` | int | `2` | タグクラウドに出す最小出現回数 |

## インデックス可否

| キー | 型 | 初期値 | 説明 |
|------|-----|--------|------|
| `site.noindex` | bool | `false` | `true` で `<meta name="robots" content="noindex, nofollow">` を出力 |

> [!IMPORTANT]
> 本番公開時は必ず `site.noindex: false` にしてください。開発ブランチで `true` にしている場合、誤って本番にデプロイすると検索結果から消えます。

## 設定例

```yaml
site:
  name: "md2docs"
  description: "A file-based documentation site powered by md2docs."
  url: "https://docs.example.com"
  timezone: "Asia/Tokyo"
  entries_per_page: 10
  home_entries_per_category: 5
  tag_cloud_min_count: 2
  excerpt_length: 200
  date_format: "Y/m/d"
  theme: "docs"
  noindex: false
```

## 環境別の切り分け

開発・ステージング・本番で異なる設定が必要な場合、`config/site.local.yaml` のような別ファイルに書き、`Application.php` でロード順を制御するパターンを推奨します（将来対応予定）。

> [!NOTE]
> 現状は単一ファイルを前提にしています。環境別設定が必要なプロジェクトでは、CI のビルド時にファイルを差し替えるのが現実的です。
