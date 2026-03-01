# 戦略概要（BOSS用）

> 元資料: `ai-agent-organization/inbox/X×note戦略の草案.md`
> 概要版: `ai-agent-organization/shared/knowledge/x-note-brand-strategy.md`

---

## ファネル全体像

```
X投稿（問いを立てる・症状を言語化する）
    ↓  [X→note誘導: 週2回まで、「まとめました」程度]
noteで答えを置く（原因と解決策）
    ↓  [note内回遊: 3点リンク（前・次・シリーズ一覧）]
note内でシリーズを回遊する
    ↓  [無料記事3本で信頼構築]
無料記事末尾から有料記事へ
    ↓  [CTAテンプレートA/B/C]
有料教材（[YOUR_PRICE]）の購買
    ↓  [継続商品誘導テンプレート]
継続課金商品への誘導（[YOUR_PRICE]）
```

---

## エージェント別の戦略レイヤー担当

| エージェント | 担当する戦略レイヤー | 主な役割 |
|------------|------------------|---------|
| **NOTE_GUNSHI** | 全レイヤーの戦略立案 | ファネル設計・X/note運用戦略の壁打ち・KPI・PDCA |
| **X_POST_CREATOR** | ファネル第1層（認知） | X投稿4カテゴリ・週間カレンダー・初動設計・リプライ戦略 |
| **NOTE_CREATOR** | ファネル第2〜3層（信頼構築） | note記事7ステップ構造・タイトル設計・シリーズ設計 |
| **ARTICLE_STYLIST** | ファネル第3〜4層（購買導線） | 無料記事末尾の有料誘導文・回遊3点リンク・継続商品誘導 |
| **ARTICLE_REVIEWER** | 全レイヤーの品質管理 | ブランディング逸脱チェック・リード文評価・余白設計評価 |
| **DATA_ANALYST** | ファネル全体のKPI測定 | 各層の数値計測・遷移率分析・改善提案 |

---

## エージェント連携フロー

### X案件の橋渡し判断基準

**X投稿作成依頼が来た場合**:

1. まずX_POST_CREATORに回す
2. X_POST_CREATORが参照する `x-operation-guide.md` の4カテゴリに基づいて投稿を設計
3. カテゴリA（症状描写型）またはD（実験比較型）でnote誘導が必要な場合 → 対応するnote記事があるか確認
4. note記事が未作成の場合 → NOTE_CREATORにも並列でnote記事を依頼（パイプラインではなく並列型）

### note案件の橋渡し判断基準

**note記事作成依頼が来た場合**:

1. NOTE_CREATORに記事を作成させる（7ステップ構造遵守）
2. 完成後 → ARTICLE_REVIEWERでブランドチェック（brand-check-criteria.mdのチェックリスト確認）
3. レビュー通過後 → ARTICLE_STYLISTで装飾・CTA配置・回遊3点リンク挿入
4. 同時にX_POST_CREATORでnote宣伝投稿を作成（並列実行可）

### 複合案件（X+note同時）の処理パターン

```
依頼受領
    ↓
BOSS: タスク分解
    ↓
並列実行:
  ├── NOTE_CREATOR: note記事作成
  └── X_POST_CREATOR: X投稿作成（カテゴリA症状描写型 + note誘導あり）
    ↓
NOTE_CREATORの記事完成後:
  ├── ARTICLE_REVIEWER: レビュー
  └── （並列）X_POST_CREATOR: note宣伝投稿の更新（URLが決まったら）
    ↓
ARTICLE_STYLIST: 装飾・CTA・回遊リンク挿入
```

---

## チームメイトへの指示時に確認すること

各エージェントにタスクを振る際、以下を意識する。

### NOTE_GUNSHIへ（戦略壁打ち・企画立案時）
- `account-strategy-v2.md` に今回の草案の全体像を構造化済み
- 戦略判断は5層FWに基づく
- X運用4カテゴリと週間カレンダーを活用した企画提案ができる

### NOTE_CREATORへ（記事作成時）
- `note-operation-guide.md` の7ステップ構造に従う
- タイトル設計はNG/OK例を参照
- 無料記事の場合: 必ず末尾に有料誘導文を入れること

### X_POST_CREATORへ（X投稿作成時）
- `x-operation-guide.md` の4カテゴリから適切なものを選択
- note誘導有無の判断基準を必ず確認してから作成
- 週間カレンダーとの整合性も確認

### ARTICLE_REVIEWERへ（レビュー時）
- `brand-check-criteria.md` のブランドチェックリストを追加評価軸として使う
- 絶対に使わない表現リストに引っかかる場合は必ず指摘

### ARTICLE_STYLISTへ（装飾・CTA配置時）
- `cta-and-navigation.md` の3パターンのCTAテンプレートから選択
- 回遊3点リンクは必ず末尾に設置
- 有料記事には継続商品誘導を設置

---

## 重要な制約（絶対に守る）

- X投稿でのnote誘導は週2回まで
- 絶対に使わない表現（稼ぎ方・月〇万円・収益化 等）を含む成果物はリテイク
- [YOUR_NICHE]固有の専門用語を多用している場合はリテイク（ターゲット読者が理解できない可能性）
- CTA配置が強引な場合（「今すぐ買ってください」等）はリテイク
