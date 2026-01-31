# /next-phase コマンド

指定REQの現在Phaseを承認し、次のPhaseを開始します。

## 使用方法

```
/next-phase REQ-YYYY-NNN
```

## 引数

- `REQ-YYYY-NNN`: 依頼番号（必須）

## 実行内容

### 1. 現在Phase確認

`documents/REQ-YYYY-NNN/00_進捗管理.md` を読み込み、現在のPhase状態を確認。

### 2. 成果物チェック

現在Phaseの成果物が存在するか確認:

| Phase | 成果物チェック |
|-------|---------------|
| 1 | `inputs/REQ-YYYY-NNN/ヒアリング記録.md` |
| 2 | `documents/REQ-YYYY-NNN/01_要求定義書.md` |
| 3 | `documents/REQ-YYYY-NNN/02_設計書.md` |
| 4 | `documents/REQ-YYYY-NNN/03_WBS.md` |
| 5 | `outputs/REQ-YYYY-NNN/` フォルダ |
| 6 | `documents/REQ-YYYY-NNN/04_完了報告.md` |
| 7 | `Issue/Issue-list.md` 更新確認 |

### 3. Phase状態更新

`00_進捗管理.md` を更新:
- 現在Phase: ✅ + 承認日
- 次Phase: 🔄
- ステータス更新

### 4. 次Phaseガイダンス

次Phaseの作業内容を表示。

---

## Phase別ガイダンス

### Phase 1 → 2（ヒアリング完了 → 要求定義）

```
Phase 1（ヒアリング）が承認されました。

次は Phase 2（要求定義）です。
以下を作成してください:
- documents/REQ-YYYY-NNN/01_要求定義書.md

テンプレート: templates/01_要求定義書.md
```

### Phase 2 → 3（要求定義 → 設計）

```
Phase 2（要求定義）が承認されました。

次は Phase 3（設計）です。
以下を作成してください:
- documents/REQ-YYYY-NNN/02_設計書.md

テンプレート: templates/02_設計書.md
```

### Phase 3 → 4（設計 → WBS）

```
Phase 3（設計）が承認されました。

次は Phase 4（WBS）です。
以下を作成してください:
- documents/REQ-YYYY-NNN/03_WBS.md

テンプレート: templates/03_WBS.md
```

### Phase 4 → 5（WBS → 実装）

```
Phase 4（WBS）が承認されました。

次は Phase 5（実装）です。
以下を作成してください:
- outputs/REQ-YYYY-NNN/（成果物フォルダ）

WBSに従って実装を進めてください。
```

### Phase 5 → 6（実装 → 完了報告）

```
Phase 5（実装）が承認されました。

次は Phase 6（完了報告）です。
以下を作成してください:
- documents/REQ-YYYY-NNN/04_完了報告.md
- knowledge/lessons/ に教訓を追記

テンプレート: templates/04_完了報告.md
```

### Phase 6 → 7（完了報告 → Issue管理）

```
Phase 6（完了報告）が承認されました。

次は Phase 7（Issue管理）です。
以下を実行してください:
1. Issue/Issue-list.md に今後の課題を起票
2. 優先度（P0-P3）を設定
3. P1 Issueを束ねて次REQ候補を提示
4. lessons/ から business/ へルール昇格
```

### Phase 7 → REQ完了

```
Phase 7（Issue管理）が承認されました。

REQ-YYYY-NNN は完了です。
```

---

## エラー処理

### 成果物が見つからない場合

```
⚠️ Phase X の成果物が見つかりません。

必要なファイル:
- [ファイルパス]

先に成果物を作成してから /next-phase を実行してください。
```
