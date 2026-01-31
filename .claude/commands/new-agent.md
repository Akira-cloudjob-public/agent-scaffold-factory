# /new-agent コマンド

汎用エージェントテンプレートを指定した場所に払い出します。

## 使用方法

```
/new-agent [エージェント名] [出力先パス]
```

## 引数

- `エージェント名`: 払い出すエージェントの名前（必須）
- `出力先パス`: エージェントを配置するディレクトリ（必須）

## 実行内容

### 1. 出力先の確認

```
出力先ディレクトリが存在しない場合は作成します。
既に存在する場合は上書き確認を行います。
```

### 2. テンプレートのコピー

`src/agent-framework/` の内容を出力先にコピー:

```
src/agent-framework/
├── CLAUDE.md            → [出力先]/CLAUDE.md
├── .claude/commands/    → [出力先]/.claude/commands/
├── templates/           → [出力先]/templates/
├── knowledge/           → [出力先]/knowledge/
├── documents/           → [出力先]/documents/
├── inputs/              → [出力先]/inputs/
├── outputs/             → [出力先]/outputs/
└── Issue/               → [出力先]/Issue/
```

### 3. CLAUDE.md のカスタマイズ

払い出されたエージェントの CLAUDE.md を更新:
- エージェント名を設定
- 作成日を記録

### 4. 管理簿への記録

`src/agent-management/エージェント管理簿.md` に記録を追加:
- 払い出し日時
- エージェント名
- 出力先パス

### 5. 完了報告

```markdown
## エージェント払い出し完了

**エージェント名**: [エージェント名]
**出力先**: [出力先パス]
**払い出し日時**: YYYY-MM-DD HH:MM:SS

### 次のステップ

1. 出力先に移動してエージェントを起動:
   ```bash
   cd [出力先パス]
   claude
   ```

2. 新しい依頼を開始:
   ```
   /start-req REQ-YYYY-NNN
   ```

3. 必要に応じて専門スキルを追加:
   - `knowledge/business/` に業務ルールを追加
   - `.claude/commands/` にカスタムコマンドを追加
```

---

## 実行例

```
ユーザー: /new-agent データ分析エージェント ~/projects/data-analyst

Claude:
## エージェント払い出し完了

**エージェント名**: データ分析エージェント
**出力先**: ~/projects/data-analyst
**払い出し日時**: 2026-02-01 10:00:00

### 次のステップ

1. 出力先に移動してエージェントを起動:
   ```bash
   cd ~/projects/data-analyst
   claude
   ```

2. 新しい依頼を開始:
   ```
   /start-req REQ-2026-001
   ```

3. BigQuery スキルを追加する場合:
   - `.claude/commands/bigquery.md` を作成
   - `knowledge/technical/bigquery.md` を作成
```

---

## 注意事項

- 払い出されたエージェントは独立して動作します
- 元のテンプレートへの変更は払い出し済みエージェントには反映されません
- カスタマイズは払い出し先で行ってください
