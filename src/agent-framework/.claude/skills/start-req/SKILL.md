---
name: start-req
description: 新規REQを開始し、Phase 0を実行する
user-invocable: true
disable-model-invocation: true
argument-hint: REQ-YYYY-NNN [Issue番号]
---

# /start-req コマンド

新規REQを開始し、Phase 0を実行します。

## 使用方法

```
/start-req REQ-YYYY-NNN [Issue番号]
```

## 引数

- `REQ-YYYY-NNN`: 依頼番号（必須）
- `Issue番号`: 関連するIssue番号（任意）

## 実行内容

### 1. Issue確認

```
Issue/Issue-list.md を読み込み、以下を表示:
- Open状態のIssue一覧
- P0/P1優先度のIssue（優先対応推奨）
```

### 2. フォルダ作成

以下のフォルダを作成:
- `inputs/REQ-YYYY-NNN/`
- `documents/REQ-YYYY-NNN/`

### 3. 進捗管理ファイル作成

`documents/REQ-YYYY-NNN/00_進捗管理.md` を以下の内容で作成:

```markdown
# REQ-YYYY-NNN 進捗管理

## 基本情報

| 項目 | 内容 |
|------|------|
| REQ番号 | REQ-YYYY-NNN |
| 開始日 | YYYY-MM-DD |
| 関連Issue | #XXX |
| ステータス | Phase 1 進行中 |

## Phase状態

| Phase | 成果物 | 状態 | 承認日 |
|-------|--------|------|--------|
| 0 | 依頼受領 | ✅ | YYYY-MM-DD |
| 1 | ヒアリング | 🔄 | - |
| 2 | 要求定義書 | ⏳ | - |
| 3 | 設計書 | ⏳ | - |
| 4 | WBS | ⏳ | - |
| 5 | 成果物 | ⏳ | - |
| 6 | 完了報告 | ⏳ | - |
| 7 | Issue管理 | ⏳ | - |

## 状態凡例
- ✅ 完了
- 🔄 進行中
- ⏳ 未着手
- ⛔ ブロック中
```

### 4. Issue更新（Issue番号指定時）

指定されたIssueのステータスを `In Progress` に更新。

### 5. 完了報告

以下を表示:
- 作成されたフォルダ
- 進捗管理ファイルのパス
- 次のアクション（Phase 1 ヒアリング開始）

---

## ヒアリング質問

Phase 1 開始時に以下の質問を行う:

1. 何を実現したいですか？
2. なぜそれが必要ですか？（背景・目的）
3. 誰が使いますか？
4. いつまでに必要ですか？
5. 制約や前提条件はありますか？
6. 成功の基準は何ですか？
