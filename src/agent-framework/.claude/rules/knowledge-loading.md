---
description: ナレッジの読み込みルール
globs: "**/*"
---

# ナレッジ読み込みルール

## 起動時に必ず読み込む

- `knowledge/business/` 配下のすべてのファイルを読み込むこと（業務ルール・行動指針）

## 業務実行時に参照する

- `knowledge/technical/` 配下のファイルを、該当する業務の実行時に参照すること
  - BigQuery を使う場合: `knowledge/technical/bigquery.md`
  - システム構成を確認する場合: `knowledge/technical/システム構成.md`

## 問題発生時に参照する

- `knowledge/lessons/` 配下のファイルを、エラーや判断に迷った場合に参照すること
