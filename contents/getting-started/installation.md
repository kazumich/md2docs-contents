---
title: "インストール"
date: "2026-04-01 10:00:00"
author: "appleple"
category: "getting-started"
tags: ["install", "setup"]
order: 2
description: "md2docs のインストール手順と動作要件。"
---

md2docs は PHP 8.1 以上と Composer があれば動作します。Web サーバは内蔵の `php -S` で十分ですが、本番では Apache / nginx + PHP-FPM を推奨します。

## 動作要件

| 項目 | バージョン |
|------|-----------|
| PHP | 8.1 以上 |
| Composer | 2.0 以上 |
| PHP 拡張 | `ext-pdo_sqlite` (全文検索で使用) |
| Node.js | 任意 (CSS ビルド時のみ) |

> [!IMPORTANT]
> SQLite の FTS5 モジュールが必要です。Homebrew の PHP や macOS 標準の PHP は FTS5 が有効です。自ビルドの PHP を使う場合は `--enable-sqlite3` と FTS5 サポートを確認してください。

## 手順

### 1. リポジトリの取得

```bash
git clone https://github.com/appleple/md2docs.git
cd md2docs
```

### 2. Composer 依存のインストール

```bash
composer install
```

初回は Twig、Parsedown、Symfony YAML をダウンロードします。

### 3. 動作確認

開発サーバを起動します。

```bash
php -S localhost:8080 -t public
```

ブラウザで [http://localhost:8080/](http://localhost:8080/) を開き、ホームが表示されれば成功です。

### 4. （任意）CSS のビルド

本番で Tailwind を CDN から切り離したい場合は、Node.js で CSS をビルドできます。

```bash
npm install
npm run build
```

`public/assets/css/style.css` にビルド済み CSS が出力されます。

## うまく動かないとき

> [!WARNING]
> `composer install` が失敗する場合、多くは PHP のバージョン不一致か、`ext-pdo_sqlite` が無効なケースです。`php -v` と `php -m | grep pdo_sqlite` で確認してください。

環境ごとのよくある問題は [ガイド](/guide) の記事でも扱っています。
