# md2docs-contents

[md2docs](https://github.com/kazumich/md2docs) で公開しているドキュメントサイトのコンテンツリポジトリです。

このリポジトリには記事 Markdown とサイト構造定義しか入っていません。レンダリングは [md2docs](https://github.com/kazumich/md2docs) エンジン側に任せ、**執筆者はこのリポジトリだけ clone すれば十分**です。PHP も Composer も Node.js もインストール不要。

## クイックスタート（執筆者向け）

```bash
git clone https://github.com/kazumich/md2docs-contents.git
cd md2docs-contents
```

1. `contents/` 配下の Markdown を編集する（または新規作成）
2. 普通の git 操作でコミット → push
3. **`main` への push で自動デプロイ**（GitHub Actions が XSERVER に FTP）
4. 数分後、本番サイトに反映される

セットアップは以上。ローカル PHP サーバを動かす必要はありません。

## ディレクトリ構成

```
md2docs-contents/
├── contents/               # 記事本体 (Markdown)
│   ├── getting-started/
│   │   ├── introduction.md
│   │   ├── installation.md
│   │   └── ...
│   ├── guide/
│   │   ├── writing-articles.md
│   │   ├── basics/         # サブカテゴリ可
│   │   │   └── ...
│   │   └── ...
│   └── reference/
│       └── ...
├── categories.yaml         # トップレベル & サブのラベル・並び順定義
└── .github/workflows/
    └── deploy.yml          # 自動 FTP デプロイ
```

URL は `contents/{セクション}/{ファイル名}.html` の形式でそのまま反映：

| ファイル | URL |
|---------|-----|
| `contents/guide/installation.md` | `/guide/installation.html` |
| `contents/guide/basics/setup.md` | `/guide/basics/setup.html` |

## 記事の書き方

ファイル先頭に YAML フロントマター、本文を Markdown で書きます。

```markdown
---
title: "ページタイトル"
date: "2026-04-25 12:00:00"
order: 1
description: "一覧やサイドバーで表示する説明文"
tags: ["intro", "setup"]
---

# 本文

普通の Markdown です。コードブロック、表、リスト、リンクが使えます。

## GitHub 風 callout

> [!NOTE]
> 補足情報（青）

> [!TIP]
> ヒント（緑）

> [!IMPORTANT]
> 重要（紫）

> [!WARNING]
> 注意（黄）

> [!CAUTION]
> 警告（赤）

## 記事間リンク

`.md` で書けば自動で `.html` に変換されます。

[インストール](/getting-started/installation.md) を参照してください。
```

執筆ルールの詳細は本番サイトの「ガイド」セクションを参照してください。

## 推奨ワークフロー

### 単発の修正

```bash
# 1. main ブランチで作業
git pull origin main
$EDITOR contents/guide/some-article.md

# 2. コミットして push
git add contents/guide/some-article.md
git commit -m "fix: typo in some-article"
git push origin main
```

→ Actions が走り、数分で本番反映。

### 複数人でレビューしたい記事

```bash
# 1. 作業ブランチを作る
git checkout -b add/new-feature-doc
$EDITOR contents/guide/new-feature.md
git add . && git commit -m "add: new-feature.md"
git push -u origin add/new-feature-doc

# 2. GitHub で Pull Request を作成 → レビュー後マージ
```

→ main にマージされると Actions が走り、本番反映。

> [!NOTE]
> このリポジトリは GitHub Web UI からも直接編集可能です。`.md` ファイルを開いて鉛筆アイコンをクリックすれば、ブラウザだけで編集 → コミットができます。Markdown プレビューも GitHub 上で見られます。

## GitHub Secrets の設定（初回セットアップのみ）

リポジトリ管理者が一度だけ実施します。

**Settings → Secrets and variables → Actions → New repository secret** で以下を登録：

| Secret 名 | 値 |
|----------|-----|
| `FTP_SERVER` | XSERVER の FTP ホスト（例: `svXXXX.xserver.jp`） |
| `FTP_USERNAME` | FTP ユーザー名 |
| `FTP_PASSWORD` | FTP パスワード |
| `FTP_DEPLOY_PATH` | デプロイ先絶対パス（例: `/example.com/public_html/git2docs/`） |

設定後、`main` への push で自動デプロイが走ります。

## ローカルプレビュー（任意・エンジニア向け）

実機 XSERVER に上げる前にローカルで確認したい場合のみ：

```bash
# 1. md2docs エンジン側を clone
cd ..
git clone https://github.com/kazumich/md2docs.git
cd md2docs

# 2. 依存をインストール
composer install
npm install
npm run build

# 3. このリポジトリのコンテンツをエンジンに差し込む
rm -rf contents config/categories.yaml
ln -s ../md2docs-contents/contents contents
ln -s ../md2docs-contents/categories.yaml config/categories.yaml

# 4. ローカルサーバ起動
php -S localhost:8080 -t public
```

ブラウザで http://localhost:8080/ を開けば自分のコンテンツでプレビューできます。

ただし**この手順は必須ではありません**。Markdown は GitHub Web UI でプレビューできますし、変更はブランチ・PR で確認できます。
