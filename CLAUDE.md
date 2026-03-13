# AI Agent Organization - Agent Teams 設定

このプロジェクトは、AIエージェント組織を構築・運用するためのテンプレートです。
Claude Code Agent Teams（Opus 4.6）に最適化された構成で動作します。

---

## チーム構成

| 役割 | エージェント（名前） | subagent_type | 担当領域 |
|------|---------------------|---------------|----------|
| Team Lead | BOSS（司） | BOSS | タスク管理・チーム調整・戦略判断 |
| Teammate | NOTE_CREATOR（紡） | NOTE_CREATOR | note記事作成 |
| Teammate | ARTICLE_REVIEWER（冴） | ARTICLE_REVIEWER | 記事レビュー・評価 |
| Teammate | ARTICLE_STYLIST（彩葉） | ARTICLE_STYLIST | 記事装飾・CTA配置 |
| Teammate | DATA_ANALYST（鑑） | DATA_ANALYST | データ収集・分析 |
| Teammate | X_POST_CREATOR（響也） | X_POST_CREATOR | X投稿作成 |
| Teammate | ARCHITECT（匠） | ARCHITECT | プロンプト設計・スキル作成 |
| Teammate | GENESIS（創） | GENESIS | エージェント設計・作成 |
| Teammate | GUNSHI（官兵衛） | GUNSHI | 副業全体戦略・参謀コンサルタント |
| Teammate | OVERSEER（整） | OVERSEER | ディレクトリ構造管理・監査 |
| Teammate | MAIL_CREATOR（文） | MAIL_CREATOR | メールマガジン作成（通常・セールス） |

---

## タスクルーティング & スキル自動発動

| キーワード | エージェント | スキル |
|-----------|-------------|--------|
| 記事作成、note記事、ブログ | NOTE_CREATOR → ARTICLE_STYLIST（自動連動） | `note-creation` → 装飾 |
| 記事レビュー、評価、レビューして、コンテンツチェック | ARTICLE_REVIEWER | `content-review` |
| 記事装飾、CTA、ハッシュタグ | ARTICLE_STYLIST | - |
| データ収集、データ分析、ダッシュボード | DATA_ANALYST | - |
| X分析、analytics、X運用の改善、ツイートの数字 | DATA_ANALYST | `x-analytics-analysis` |
| X投稿、ツイート、note宣伝 | X_POST_CREATOR | - |
| プロンプト、スキル作成、スキル化、SKILL.md | ARCHITECT | `skill-creator` / `prompt-*` |
| エージェント作成、新しいエージェント | GENESIS | - |
| 壁打ち、戦略、方向性、ポジショニング、商品設計 | GUNSHI | `note-strategy-sparring` |
| コンテンツ企画、記事のネタ、タイトル案、何を書くべきか | GUNSHI | `note-content-planning` |
| KPI、PDCA、数字を振り返り、改善点、今月の結果 | GUNSHI | `note-kpi-pdca` |
| 競合分析、市場調査、他の人はどうやっている | GUNSHI | `note-competitor-analysis` |
| 今日何するべき、優先タスク、今週のタスク、何から始める | BOSS + GUNSHI | `daily-strategy` |
| ディレクトリ監査、構造チェック、クリーンアップ、ヘルスチェック、整理整頓 | OVERSEER | `directory-audit` / `health-report` |
| 組織を作って、セットアップして、初期化して | BOSS | `setup-org` |
| 状況報告、ステータス確認、今どうなってる | BOSS | `status-report` |
| タスク依頼、これやって、実行して | BOSS | `task-request` |
| 計画、連携、チーム、調整、方針 | BOSS | - |
| メルマガ作成、メルマガを書いて、メール配信 | MAIL_CREATOR | `regular-newsletter` |
| セールスメルマガ、ステップメール、3日間メール、セールスシナリオ | MAIL_CREATOR | `sales-newsletter` |

---

## 並列実行パターン

```
記事作成（必須連動）: NOTE_CREATOR → ARTICLE_STYLIST（常にセット）
フルパイプライン:      NOTE_CREATOR → ARTICLE_REVIEWER → ARTICLE_STYLIST
並列:                 NOTE_CREATOR + X_POST_CREATOR（同時作成）
ファンアウト:          BOSS → NOTE_CREATOR + X_POST_CREATOR + DATA_ANALYST
```

---

## 共通品質基準

### knowledge/ 参照ルール
- タスク開始時に該当エージェントの `learnings.md` を確認（weight 5以上は最優先）
- `shared/knowledge/` の組織共通知識を参照

### 成果物の保存
- 保存先: `ai-agent-organization/workspace/YYYY-MM-DD_NN/[type]-[topic].md`
  - `NN`: タスク開始時に `workspace/YYYY-MM-DD_*` の既存フォルダ数を確認し、次の連番（01, 02...）を採番
  - 同じ依頼内の複数成果物は同じセッションフォルダ（`YYYY-MM-DD_NN/`）に格納
- タスク完了時に自動保存

### フィードバックサイクル
1. タスク完了後、ユーザーにフィードバックを依頼
2. フィードバックを `learnings.md` に記録（重みづけシステム対応）
3. `HISTORY.md` に履歴を記録

---

## ディレクトリ構造

```
ai-agent-organization/
├── organization/    # エージェント別知識ベース
├── shared/
│   ├── knowledge/   # 組織共通知識
│   └── templates/
└── workspace/       # 成果物保存先
```

---

## クイックスタート

1. 「〇〇の組織を作って」 → 組織構築
2. 「タスク依頼: [内容]」 → タスク実行
3. 「状況報告して」 → ステータス確認
4. 「今日何するべき？」 → BOSSとGUNSHIがデイリータスクを提案
5. 「戦略を考えたい」 → GUNSHIがビジネス戦略全体を壁打ち
