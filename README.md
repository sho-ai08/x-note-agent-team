# x-note Agent Team Template

**note×X（旧Twitter）の収益化を自動化する、Claude Code Agent Teamsテンプレート**

Claude Code の Agent Teams 機能（Opus 4.6）に最適化された、10体のAIエージェントが連携して動作する組織テンプレートです。

---

## 何ができるのか

- note記事の作成・レビュー・装飾を自動パイプライン処理
- X投稿（宣伝・オリジナル・長文）を並列生成
- KPI分析・PDCA・コンテンツ企画・競合調査を一括依頼
- 副業収益化の戦略壁打ち・日次タスク提案

---

## エージェント一覧

| 役割 | エージェント | 担当 |
|------|------------|------|
| Team Lead | **BOSS（司）** | タスク管理・チーム調整・戦略判断 |
| Teammate | **NOTE_CREATOR（紡）** | note記事作成 |
| Teammate | **ARTICLE_REVIEWER（冴）** | 記事レビュー・評価 |
| Teammate | **ARTICLE_STYLIST（彩葉）** | 記事装飾・CTA配置・ハッシュタグ |
| Teammate | **DATA_ANALYST（鑑）** | データ収集・X analytics分析 |
| Teammate | **X_POST_CREATOR（響也）** | X投稿作成 |
| Teammate | **ARCHITECT（匠）** | プロンプト設計・スキル作成 |
| Teammate | **GENESIS（創）** | エージェント設計・作成 |
| Teammate | **NOTE_GUNSHI（官兵衛）** | 副業全体戦略・参謀コンサルタント |
| Teammate | **OVERSEER（整）** | ディレクトリ構造管理・監査 |

---

## クイックスタート

### 1. リポジトリをクローン

```bash
git clone https://github.com/sho-ai08/x-note-agent-team.git
cd x-note-agent-team
```

### 2. 自分の情報を設定

`ai-agent-organization/SETUP-GUIDE.md` に従って、以下を入力する：

- Xアカウント・noteアカウント情報
- ターゲット読者・ペルソナ定義
- 文体・トーン・一人称
- 権威性・実績
- 商品・マネタイズ設計
- コンテンツテーマ・専門領域

### 3. Claude Codeで使い始める

```bash
# 副業戦略を相談したい
claude "戦略を考えたい"

# note記事を作る（→ ARTICLE_STYLISTまで自動連動）
claude "note記事を書いて：[テーマ]"

# X投稿とnote記事を同時作成
claude "note記事とX投稿を同時に作って：[テーマ]"

# 今日やるべきことを確認
claude "今日何するべき？"
```

---

## タスクルーティング

| キーワード | 担当エージェント | スキル |
|-----------|----------------|--------|
| 記事作成、note記事、ブログ | NOTE_CREATOR → ARTICLE_STYLIST（自動連動） | `note-creation` |
| 記事レビュー、評価、レビューして | ARTICLE_REVIEWER | `content-review` |
| 記事装飾、CTA、ハッシュタグ | ARTICLE_STYLIST | - |
| データ収集、データ分析 | DATA_ANALYST | - |
| X分析、analytics、ツイートの数字 | DATA_ANALYST | `x-analytics-analysis` |
| X投稿、ツイート、note宣伝 | X_POST_CREATOR | - |
| プロンプト、スキル作成、SKILL.md | ARCHITECT | `skill-creator` / `prompt-*` |
| エージェント作成 | GENESIS | - |
| 壁打ち、戦略、方向性、商品設計 | NOTE_GUNSHI | `note-strategy-sparring` |
| コンテンツ企画、記事のネタ、タイトル案 | NOTE_GUNSHI | `note-content-planning` |
| KPI、PDCA、今月の結果、改善点 | NOTE_GUNSHI | `note-kpi-pdca` |
| 競合分析、市場調査 | NOTE_GUNSHI | `note-competitor-analysis` |
| 今日何するべき、優先タスク | BOSS + NOTE_GUNSHI | `daily-strategy` |
| ディレクトリ監査、ヘルスチェック、整理整頓 | OVERSEER | `directory-audit` / `health-report` |
| 状況報告、ステータス確認 | BOSS | `status-report` |
| タスク依頼、これやって | BOSS | `task-request` |

---

## 並列実行パターン

```
記事作成（必須連動）:  NOTE_CREATOR → ARTICLE_STYLIST（常にセット）
フルパイプライン:      NOTE_CREATOR → ARTICLE_REVIEWER → ARTICLE_STYLIST
並列作成:             NOTE_CREATOR + X_POST_CREATOR（同時生成）
ファンアウト:          BOSS → NOTE_CREATOR + X_POST_CREATOR + DATA_ANALYST
```

---

## スキル一覧

`.claude/skills/` に収録されている自動発動スキル：

| カテゴリ | スキル |
|---------|--------|
| note作成 | `note-creation`, `article-structure`, `note-content-planning` |
| 戦略・分析 | `note-strategy-sparring`, `note-kpi-pdca`, `note-competitor-analysis`, `x-analytics-analysis` |
| レビュー | `content-review` |
| X投稿 | `x-note-promo`, `x-original-post`, `x-long-post`, `x-casual-announcement` |
| プロンプト | `prompt-creator-unified`, `prompt-improver`, `prompt-analyzer`, `prompt-tester`, `skill-creator` |
| 組織管理 | `directory-audit`, `health-report`, `cleanup-proposal`, `status-report`, `setup-org` |
| ユーティリティ | `summarizer`, `rewriter`, `text-converter`, `transcript-formatter` |
| タスク管理 | `task-request`, `task-manager`, `task-analyzer`, `daily-strategy` |

---

## ディレクトリ構造

```
x-note-agent-team/
├── CLAUDE.md                          # エージェント組織設定（Claude Code読み込み）
├── ai-agent-organization/
│   ├── SETUP-GUIDE.md                 # 初期セットアップガイド
│   ├── organization/                  # エージェント別知識ベース
│   │   ├── BOSS/                      # Team Lead
│   │   ├── OVERSEER/                  # 構造管理
│   │   ├── hr-tech/                   # ARCHITECT, GENESIS
│   │   └── operations/                # NOTE_CREATOR, ARTICLE_REVIEWER, ARTICLE_STYLIST,
│   │                                  # DATA_ANALYST, X_POST_CREATOR, NOTE_GUNSHI
│   ├── shared/
│   │   ├── knowledge/                 # 組織共通知識（ブランド戦略・アンチAIリライトなど）
│   │   └── templates/                 # エージェント・プロンプトテンプレート
│   ├── system/
│   │   └── config.yaml               # システム設定
│   └── workspace/                     # 成果物保存先（YYYY-MM-DD_NN/形式）
│
└── .claude/
    ├── agents/                        # Claude Code Agent定義（10体）
    └── skills/                        # スキル定義（28スキル）
```

---

## 成果物の保存

タスク完了後、成果物は以下のパスに自動保存される：

```
ai-agent-organization/workspace/YYYY-MM-DD_NN/[type]-[topic].md
```

同一セッション内の複数成果物は同じフォルダ（`YYYY-MM-DD_NN/`）にまとめられる。

---

## 動作環境

- **Claude Code CLI**（必須）
- **モデル**: Claude Opus 4.6（Agent Teams最適化）

---

## ライセンス

MIT

---

**Powered by Claude Code Agent Teams**
