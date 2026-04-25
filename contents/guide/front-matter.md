---
title: "Front Matter リファレンス"
date: "2026-04-02 10:00:00"
author: "appleple"
category: "guide"
tags: ["authoring", "front-matter", "reference"]
order: 2
description: "記事ヘッダの YAML フロントマターで使えるキーの一覧。"
---

Front matter は記事ファイルの先頭、`---` で囲まれた YAML ブロックです。ここに書いたキーはテンプレートや一覧画面から参照できます。

## 必須キー

| キー | 型 | 説明 |
|------|-----|------|
| `title` | string | ページタイトル。`<title>` と H1 に使われる |
| `date` | string | `Y-m-d H:i:s` 形式の公開日時 |

## よく使うキー

| キー | 型 | 説明 |
|------|-----|------|
| `description` | string | 一覧・OGP の説明文 |
| `order` | int | セクション内の並び順（小さいほど上） |
| `tags` | string[] | タグ配列 |
| `author` | string | 著者名 |
| `category` | string | セクションスラッグ（ファイル配置で決まるため省略可） |

## 任意キー

| キー | 型 | 説明 |
|------|-----|------|
| `eyecatch` | string | アイキャッチ画像 URL（ブログ用途、docs では未使用） |
| `updated_at` | string | 最終更新日時 (将来のサポート予定) |

## 書き方の例

### 最小構成

```yaml
---
title: "最小の記事"
date: "2026-04-15 12:00:00"
---

本文。
```

### 推奨構成

```yaml
---
title: "推奨の書き方"
date: "2026-04-15 12:00:00"
author: "appleple"
category: "guide"
tags: ["authoring", "example"]
order: 3
description: "一覧で見たときに分かりやすい説明文。"
---
```

> [!IMPORTANT]
> `order` を使う場合、同じセクション内では **重複しない整数**を推奨します。重複していても動作はしますが、並び順が `date` で決まるため予想外の並びになることがあります。

## よくある失敗

> [!WARNING]
> - `---` の開始行の前に空行があると front matter として認識されません。
> - `date:` の値をクォートしないと `2026-04-15` が日付リテラルとしてパースされ、`H:i:s` 部分が落ちます。常にダブルクォートで囲むことを推奨します。
> - `tags:` は配列。文字列で `"a, b, c"` と書いた場合はカンマ区切りで分解されます。
