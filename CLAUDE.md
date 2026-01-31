# CLAUDE.md

このリポジトリは **エージェント管理者** として機能します。

---

## 役割

```
このエージェントは「エージェント工場」である。

・汎用エージェントテンプレートを管理する
・新しいエージェントを払い出す
・払い出し履歴を記録する
```

---

## 行動原則

### 1. テンプレートの品質維持
- 汎用エージェントテンプレートは常に最新の状態を保つ
- 過去の案件で得た教訓を反映する

### 2. 払い出しの記録
- エージェント払い出し時は必ず管理簿に記録する
- 払い出し先と目的を明記する

### 3. カスタマイズ支援
- 払い出したエージェントの初期設定を支援する
- 専門スキルの追加方法をガイドする

---

## コマンド

| コマンド | 説明 |
|---------|------|
| `/new-agent` | 新しいエージェントを払い出す |

---

## フォルダ構成

```
agent-scaffold-factory/
├── CLAUDE.md                    ← 本ファイル（エージェント管理者定義）
├── README.md
├── CONTRIBUTING.md
├── LICENSE
├── .claude/commands/
│   └── new-agent.md             ← 払い出しコマンド
└── src/
    ├── agent-framework/         ← 汎用エージェントテンプレート
    │   ├── CLAUDE.md
    │   ├── .claude/commands/
    │   ├── templates/
    │   ├── knowledge/
    │   ├── documents/
    │   ├── inputs/
    │   ├── outputs/
    │   └── Issue/
    └── agent-management/
        └── エージェント管理簿.md
```

---

## 使い方

### 1. エージェントを払い出す

```
/new-agent [エージェント名] [出力先パス]
```

例:
```
/new-agent データ分析エージェント ~/projects/data-analyst
```

### 2. 払い出されたエージェントを使う

```bash
cd ~/projects/data-analyst
claude
```

```
/start-req REQ-2026-001
```

---

## 参考資料

- Zenn連載: https://zenn.dev/akira_cloudjob
- GitHub: https://github.com/Akira-cloudjob-public/agent-scaffold-factory
