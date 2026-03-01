# OVERSEER MEMORY

## プロジェクト構造の重要ポイント

### エージェント自己完結化の注意点
- 各エージェントMDは自己完結型。`shared/common-workflow.md` や `shared/learnings-index.md` は現在どのエージェントからも参照されていない（孤立ナレッジ）
- `shared/knowledge/` で有効活用されているのは `noteの心得.md` と `anti-ai-rewrite-master.md` の2ファイルのみ

### 削除済みファイル
- `shared/knowledge/guidelines.md` は削除済み（styling-guidelines.mdとreview-criteria.mdに統合）
- 参照が残っているファイル: `BOSS/directives/2026-01-29_NOTE_CREATOR_improvement_directive.md`、`shared/common-workflow.md`

### inbox/ の運用
- 処理後も削除されず滞留するケースが多い。監査時は必ずチェック
- 2026-02-22時点で未処理ファイルが4件滞留

### 標準構造（2026-02-22確認）
```
エージェントディレクトリ/
├── HISTORY.md
├── learnings.md（ルート直下）
├── STATUS.yaml（存在するが形骸化の可能性あり）
└── knowledge/
    ├── knowhow/
    └── examples/（あるエージェントのみ）
```
- examples/ があるエージェント: NOTE_CREATOR, X_POST_CREATOR, ARCHITECT, ARTICLE_STYLIST

### 不要ファイル
- .DS_Store が `ai-agent-organization/` と `ai-agent-organization/shared/` に存在（要削除）
- `inbox/The-Complete-Guide-to-Building-Skill-for-Claude.pdf` は skill-building-guide.md として知識化済み（要削除）

## 学び

- エージェント構造変更時は `grep -r "旧ファイル名"` で幽霊参照を必ず確認すること
- inbox/ は毎回の監査でチェック対象に含めること
