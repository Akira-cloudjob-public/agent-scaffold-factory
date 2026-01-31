# technical/

技術知識とシステム情報を格納するフォルダです。

## 特徴

- 必要時に参照
- 技術スタックの情報を集約
- 設定値やAPIの仕様を記録

## 例

```markdown
# BigQuery 設定

## プロジェクト情報

| 項目 | 値 |
|------|-----|
| プロジェクトID | my-project-123 |
| データセット | analytics |
| リージョン | asia-northeast1 |

## よく使うクエリ

### 月次売上集計
```sql
SELECT
  FORMAT_DATE('%Y-%m', order_date) AS month,
  SUM(amount) AS total
FROM sales
GROUP BY 1
ORDER BY 1
```
```

## ファイル命名規則

```
[技術名]_[内容].md

例:
- bigquery_settings.md（BigQuery設定）
- api_specifications.md（API仕様）
- database_schema.md（データベーススキーマ）
```
