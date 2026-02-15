# エージェントフレームワーク

優秀な部下として振る舞い、人間と協働しながら成長するエージェントのプロジェクト構成です。

> **2026-02-15 更新**: Claude Code 公式の Skills 統合に合わせ、`.claude/commands/` → `.claude/skills/`（SKILL.md 形式）に移行しました。`disable-model-invocation` による自律化制御と、`.claude/rules/` によるナレッジ読み込み制御を追加しています。

---

## フォルダ構成

```
project-root/
│
├── inputs/                        # 生情報（インプット）
│   ├── _REQ-TEMPLATE/             # ★サンプル（新規依頼時にコピー）
│   │   ├── ヒアリング記録.md
│   │   └── README.md
│   └── REQ-YYYY-NNN/              # 実際の依頼
│       ├── ヒアリング記録.md
│       └── 提供資料/
│
├── knowledge/                     # 構造化知識（ナレッジ）
│   ├── templates/                 # ★ナレッジ用テンプレート
│   │   └── （案件タイプ別テンプレート）
│   ├── business/                  # 業務知識
│   ├── technical/                 # 技術知識
│   ├── people/                    # 関係者情報
│   └── lessons/                   # 過去の教訓
│
├── documents/                     # プロジェクトドキュメント
│   ├── guidelines/                # ★開発ガイドライン（共通）
│   │   └── _PLACEHOLDER.md
│   ├── _REQ-TEMPLATE/             # ★サンプル（新規依頼時にコピー）
│   │   ├── 01_要求定義書.md
│   │   ├── 02_設計書.md
│   │   ├── 03_WBS.md
│   │   └── README.md
│   └── REQ-YYYY-NNN/              # 実際の依頼
│       ├── 01_要求定義書.md
│       ├── 02_設計書.md
│       ├── 03_WBS.md
│       └── 04_完了報告.md
│
├── src/                           # 成果物
│   ├── common/                    # ★共通コンポーネント
│   ├── utils/                     # ★共通ユーティリティ
│   ├── tools/                     # ★開発支援ツール
│   ├── _REQ-TEMPLATE/             # ★サンプル（実装開始時にコピー）
│   │   ├── main.py
│   │   ├── config.py
│   │   ├── README.md
│   │   └── tests/
│   └── REQ-YYYY-NNN/              # 実際のプロジェクト
│       └── ...
│
├── templates/                     # ドキュメントテンプレート
│   ├── 00_ヒアリング記録.md
│   ├── 01_要求定義書.md
│   ├── 02_設計書.md
│   ├── 03_WBS.md
│   └── 04_完了報告.md             # ★新規追加
│
├── .claude/                       # Claude Code 設定
│   ├── skills/                    # スキル定義（SKILL.md 形式）
│   │   ├── start-req/SKILL.md     # /start-req — 依頼開始
│   │   ├── next-phase/SKILL.md    # /next-phase — 次のフェーズへ
│   │   ├── status/SKILL.md        # /status — 進捗確認
│   │   └── approve-phase/SKILL.md # /approve-phase — フェーズ承認
│   └── rules/                     # パス固有ルール
│       └── knowledge-loading.md   # knowledge/ 読み込み制御
│
├── CLAUDE.md                      # エージェント定義
└── README.md                      # このファイル
```

### ★印の説明

| マーク | 意味 |
|--------|------|
| ★サンプル | 新規作成時にコピーして使うテンプレートフォルダ |
| ★新規追加 | 今回の改良で追加されたファイル |

---

## 各フォルダの役割

### inputs/ - 生情報の保管
ヒアリングで得た生の発言、もらった資料、参照URLなど、加工前の情報をそのまま保管します。

### knowledge/ - 構造化された知識
inputsから抽出・整理した再利用可能な知識を蓄積します。エージェントは起動時にこのフォルダを読み込み、過去の知識を活用します。

### documents/ - プロジェクトドキュメント
要求定義書、設計書、WBSなど、プロジェクト管理に必要なドキュメントを格納します。
`guidelines/` には開発プロセスなどの共通ガイドラインを配置します。

### src/ - 成果物
実装したコード、スクリプト、設定ファイルなどの成果物を格納します。
- `common/`: 複数案件で再利用するコンポーネント
- `utils/`: 汎用ユーティリティ
- `tools/`: 開発支援ツール
- `REQ-YYYY-NNN/`: 案件固有の成果物

### templates/ - テンプレート
各ドキュメントのテンプレートファイルを格納します。新規案件開始時にコピーして使用します。

---

## 使い方

### 新規依頼を受けたとき

1. **依頼番号を採番**: `REQ-YYYY-NNN`（例: REQ-2026-001）

2. **サンプルフォルダをコピー**:
   ```
   inputs/_REQ-TEMPLATE/ → inputs/REQ-2026-001/
   documents/_REQ-TEMPLATE/ → documents/REQ-2026-001/
   ```

3. **ヒアリングを実施**: `inputs/REQ-2026-001/ヒアリング記録.md` に記録

4. **ドキュメントを作成**: フェーズに応じて作成
   - Phase 2: `01_要求定義書.md`
   - Phase 3: `02_設計書.md`
   - Phase 4: `03_WBS.md`

5. **実装を開始**: プロジェクトフォルダを作成
   ```
   src/_REQ-TEMPLATE/ → src/REQ-2026-001/
   ```

6. **完了報告**: `documents/REQ-2026-001/04_完了報告.md` を作成

7. **ナレッジ更新**: `knowledge/lessons/` に教訓を追記

---

## 命名規則

| 種類 | 形式 | 例 |
|------|------|-----|
| 依頼番号 | REQ-YYYY-NNN | REQ-2026-001 |

すべてのフォルダを依頼番号（REQ）で統一管理します。

---

## ライセンス

社内利用限定
