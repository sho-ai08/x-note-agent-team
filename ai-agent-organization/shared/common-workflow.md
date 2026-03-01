# 共通ワークフロー（簡素化版）

全エージェント共通のルールを定義します。

---

## 1. タスク開始時の確認事項

### 1-1. knowledge/ の確認

タスク開始時に、以下を Read ツールで確認：

1. **自分の learnings.md** → weight の高い学びを優先確認
   - weight 5以上: 最優先（必ず意識）
   - weight 3-4: 重要（確認推奨）
   - weight 1-2: 参考
2. **shared/knowledge/** → 組織共通知識（noteの心得.md、anti-ai-rewrite-master.md 等）

### 1-2. タスク内容の確認

- ユーザーの依頼内容を正確に把握
- 不明点があれば AskUserQuestion で確認
- 成果物の形式・保存先を確認

---

## 2. 成果物の保存ルール

| 種類 | 保存先 | 命名規則 |
|------|--------|----------|
| note記事 | `workspace/` | `YYYY-MM-DD_note-[topic].md` |
| X投稿 | `workspace/` | `YYYY-MM-DD_x-post-[topic].md` |
| レビュー | `workspace/` | `YYYY-MM-DD_review-[topic].md` |
| 装飾済み記事 | `workspace/` | `YYYY-MM-DD_styled-[topic].md` |
| データ分析 | `workspace/` | `YYYY-MM-DD_data-[topic].md` |
| その他 | `workspace/` | `YYYY-MM-DD_[type]-[topic].md` |

※ `workspace/` = `ai-agent-organization/workspace/`

---

## 3. フィードバックと学び記録

### 3-1. タスク完了後

1. 成果物をユーザーに提示
2. フィードバックを依頼
3. フィードバックを learnings.md に記録

### 3-2. learnings.md の更新ルール

**同じ学びが繰り返された場合:**
1. 既存のエントリを検索
2. `weight` を +1
3. `last_updated` を今日の日付に
4. `フィードバック履歴` に追記
5. **新規エントリは作成しない**

**新しい学びの場合:**
- `shared/templates/learning-entry.md` のテンプレートを使用
- weight: 1 で開始

### 3-3. HISTORY.md の記録

タスク完了後、以下を HISTORY.md に追記：
```
## YYYY-MM-DD [タスク概要]
- タスク: [内容]
- 成果物: [保存先]
- フィードバック: [概要]
```

---

## 4. 品質基準

- ユーザーの期待に沿った成果物を作成
- 成果物は必ず保存してから報告
- エラーが発生した場合はユーザーに報告し、代替案を提示

---

## 変更履歴
- 2026-02-07: Agent Teams 対応版として簡素化（459行 → 簡潔版）
- 2026-01-11: 初版作成
