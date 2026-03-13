---
name: setup-org
description: AIエージェント組織を自動構築するスキル。「組織を作りたい」「組織を作って」「セットアップして」などの依頼時に使用。
user-invocable: true
---

# 組織初期化スキル

ユーザーが組織構築を依頼しました。`ai-agent-organization/SETUP-GUIDE.md` に沿ってヒアリングを進め、組織の全ファイルをそのユーザーに最適化します。

---

## Phase 0: 事前読み込み

以下を読み込んでから開始すること：

1. `ai-agent-organization/SETUP-GUIDE.md` — ヒアリング設計書（Step 1〜7）
2. `ai-agent-organization/system/config.yaml` — 現在の設定値

---

## Phase 1: 成果物の確認（inbox チェック）

**最初に必ずこの確認をすること。**

AskUserQuestion ツールで以下を聞く：

```
これまでに書いたnote記事やX投稿のサンプルはありますか？

あれば `ai-agent-organization/inbox/` フォルダに入れてください。
サンプルをもとに文体・口調・テーマを自動抽出し、
エージェントをあなたの書き方に最適化します。

（なくてもセットアップは進められます。「なし」でも大丈夫です）
```

→ **「あり」の場合**: ユーザーがinboxに配置したら `ai-agent-organization/inbox/` を読み込み、Phase 2 の後に Phase 3a（サンプル解析）を実行する
→ **「なし」の場合**: Phase 2 に進む

---

## Phase 2: インタラクティブヒアリング

AskUserQuestion ツールで SETUP-GUIDE.md の **Step 1〜6 を1ステップずつ**確認する。

### ルール
- 1ステップ = 1回の質問（ステップ内の複数項目はまとめて聞く）
- 各ステップ後「次に進んでよいですか？」と確認してから進む
- 「未定」「後で」と答えた項目は `[未定]` プレースホルダーで残す

### ヒアリング内容（SETUP-GUIDE.md Step 1〜6 準拠）

**Step 1: アカウント基本情報**
- Xアカウント名 / ハンドルネーム（`[発信者名]` に反映）
- noteアカウントURL
- メインテーマ・発信ジャンル（`{ジャンル}` に反映）
- 発信開始時期

**Step 2: ターゲット読者・ペルソナ定義**
- メインターゲット（年齢・職業・状況）
- 読者の抱える課題
- 読者が求める価値
- 読者が自分で解決できない理由

**Step 3: 文体・トーン定義**
- 一人称（例: 僕 / 私）
- キャラクター設定
- 特徴的な口癖・頻出フレーズ
- NG表現
- 改行スタイル

**Step 4: 権威性・実績整理**
- 肩書き
- 数値実績（フォロワー数・月収・指導人数など）（`{発信者の強み②}` に反映）
- 自己開示エピソード
- 専門性の根拠（`{発信者の強み①}` に反映）

**Step 5: 商品・マネタイズ設計**
- 無料コンテンツの役割
- 有料商品①（名称・価格）（`{フロント商品}` に反映）
- 有料商品②（名称・価格）（`{ミドル商品}` `{サロン名}` に反映）
- ファネル設計
- CTAの置き方

**Step 6: コンテンツテーマ・専門領域**
- 主要テーマ 3〜5個（`{テーマタグ①②}` に反映）
- 絶対に扱わないテーマ
- 競合との差別化ポイント（`{発信者の強み③}` に反映）
- あなただけの強み

---

## Phase 3a: サンプル解析（inbox に成果物がある場合のみ）

`ai-agent-organization/inbox/` 内の全ファイルを読み込み、以下を抽出する：

### 抽出項目

**文体プロファイリング（→ writing-style-profile.md に反映）**
- 一人称の実際の使い方
- 語尾パターンと出現頻度（→ sentence-ending-patterns.md に反映）
- 特徴的な接続表現・言い回し
- 段落の長さ・改行リズム
- 感情表現・自己開示のパターン
- 読者への話しかけ方
- NG表現（AIっぽさのある表現が含まれていた場合は記録）

**コンテンツ傾向（→ analysis-methods.md・x-post-best-practices.md に反映）**
- 実際に使われているテーマ・キーワード → `{テーマタグ}` の精緻化
- 高頻度で使うフック・リード文のパターン
- CTAの置き方・表現

**note記事サンプルがある場合**
- `organization/operations/note-creator-NOTE_CREATOR/knowledge/examples/` に配置
- 見出し構成のクセ・文章構造を writing-style-profile.md に追記

**X投稿サンプルがある場合**
- `organization/operations/x-post-creator-X_POST_CREATOR/knowledge/examples/` に配置
- フック・改行・絵文字使用パターンを writing-style-profile.md に追記

---

## Phase 4: 全ファイル生成・更新

ヒアリング（＋サンプル解析）の結果をもとに、以下の**全ファイルを生成・更新**する。
既存ファイルがある場合は**完全に上書き**する（前ユーザーの情報を残さない）。

---

### グループA: 組織共通ナレッジ

| ファイルパス | 反映内容 |
|------------|---------|
| `ai-agent-organization/shared/knowledge/x-note-brand-strategy.md` | 立ち位置・訴求軸・ターゲット・ファネル・商品設計・表現スタイル（Step 1〜6 全体） |
| `ai-agent-organization/system/config.yaml` | `project.owner`（発信者名）・`project.description`（ジャンル・目的） |

---

### グループB: BOSS ナレッジ

| ファイルパス | 反映内容 |
|------------|---------|
| `ai-agent-organization/organization/BOSS/knowledge/knowhow/strategy-brief.md` | ターゲット・商品ライン・ファネル設計・発信者の強み（Step 2・4・5・6） |
| `ai-agent-organization/organization/BOSS/knowledge/knowhow/strategy-overview.md` | 全体戦略の概要・フェーズ・KPI目標（Step 5・6） |

---

### グループC: note記事作成エージェント（NOTE_CREATOR）

| ファイルパス | 反映内容 |
|------------|---------|
| `ai-agent-organization/organization/operations/note-creator-NOTE_CREATOR/knowledge/knowhow/writing-style-profile.md` | 一人称・トーン・口癖・NG表現・文章設計思想（Step 3・4 + inboxサンプル） |
| `ai-agent-organization/organization/operations/note-creator-NOTE_CREATOR/knowledge/knowhow/sentence-ending-patterns.md` | 語尾パターン一覧（inboxサンプルから抽出 or Step 3 から設計） |
| `ai-agent-organization/organization/operations/note-creator-NOTE_CREATOR/knowledge/knowhow/article-creation-process.md` | 記事作成フロー・対象テーマ・商品連動CTAの設計（Step 5・6） |
| `ai-agent-organization/organization/operations/note-creator-NOTE_CREATOR/knowledge/knowhow/creator-achievements.md` | 権威性・実績まとめ（Step 4）【新規作成】 |

---

### グループD: X投稿作成エージェント（X_POST_CREATOR）

| ファイルパス | 反映内容 |
|------------|---------|
| `ai-agent-organization/organization/operations/x-post-creator-X_POST_CREATOR/knowledge/knowhow/writing-style-profile.md` | X投稿の文体・フックパターン・体験入口フレーズ（Step 3・4 + inboxサンプル） |
| `ai-agent-organization/organization/operations/x-post-creator-X_POST_CREATOR/knowledge/knowhow/sentence-ending-patterns.md` | X投稿で使う語尾パターン（inboxサンプルから抽出 or Step 3 から設計） |
| `ai-agent-organization/organization/operations/x-post-creator-X_POST_CREATOR/knowledge/knowhow/x-post-best-practices.md` | Xでの発信ベストプラクティス・テーマ別フックパターン（Step 6 + inboxサンプル） |

---

### グループE: 記事レビューエージェント（ARTICLE_REVIEWER）

| ファイルパス | 反映内容 |
|------------|---------|
| `ai-agent-organization/organization/operations/article-reviewer-ARTICLE_REVIEWER/knowledge/knowhow/review-criteria.md` | レビューペルソナ4人の属性・評価視点・商材カテゴリ（Step 2・5）。ペルソナの「ジャンル」「商材名」を実際の値に書き換える |

---

### グループF: 記事装飾エージェント（ARTICLE_STYLIST）

| ファイルパス | 反映内容 |
|------------|---------|
| `ai-agent-organization/organization/operations/article-stylist-ARTICLE_STYLIST/knowledge/knowhow/styling-guidelines.md` | 装飾スタイル・ハッシュタグ方針・有料記事への誘導デザイン（Step 3・5） |
| `ai-agent-organization/organization/operations/article-stylist-ARTICLE_STYLIST/knowledge/knowhow/cta-and-navigation.md` | CTA文言・商品URL・関連記事導線（Step 5） |

---

### グループG: データ分析エージェント（DATA_ANALYST）

| ファイルパス | 反映内容 |
|------------|---------|
| `ai-agent-organization/organization/operations/data-analyst-DATA_ANALYST/knowledge/knowhow/analysis-methods.md` | Xアカウントのテーマ分類キーワード（`{テーマタグ①②}` を実際の値で記載）（Step 6 + inboxサンプル） |

---

### グループH: note軍師エージェント（NOTE_GUNSHI）

| ファイルパス | 反映内容 |
|------------|---------|
| `ai-agent-organization/organization/operations/note-gunshi-NOTE_GUNSHI/knowledge/knowhow/account-design.md` | Step 1〜6 の情報をまとめた戦略設計書【新規作成】 |
| `ai-agent-organization/organization/operations/note-gunshi-NOTE_GUNSHI/knowledge/knowhow/master-strategy.md` | コンテンツ戦略・KPI・商品ラインの全体設計（Step 2・5・6）【新規作成】 |

---

### グループI: スキルファイルの変数反映

成果物系スキルについて、**inboxのサンプルがある場合のみ**以下を更新する。
サンプルがない場合は変数 `{...}` のままにしておく（ユーザーが後から埋める）。

| スキルファイルパス | 更新対象の変数・セクション |
|-----------------|------------------------|
| `.claude/skills/x-long-post/SKILL.md` | `実演型コンテンツのフォーマット` 内のAI固有例（`AIで◯◯やってみた` 等）を `{ジャンル}` に合わせた例に書き換え |
| `.claude/skills/content-review/SKILL.md` | ペルソナ2「中間層」・ペルソナ4「学ぶ先探し中」の内面・評価背景をターゲット読者に合わせて書き換え |
| `.claude/skills/note-content-planning/SKILL.md` | `{フロント商品}` `{ミドル商品}` を実際の商品名・価格に書き換え |
| `.claude/skills/note-strategy-sparring/SKILL.md` | `{フロント商品}` `{ミドル商品}` を実際の商品名・価格に書き換え |
| `.claude/skills/note-competitor-analysis/SKILL.md` | `{ジャンル}` `{発信者の強み①②③}` を実際の値に書き換え |
| `.claude/skills/daily-strategy/SKILL.md` | ユーザーコンテキスト参照先が正しい knowledge ファイルを指しているか確認 |
| `.claude/skills/x-analytics-analysis/SKILL.md` | `{テーマタグ①②}` を実際のテーマキーワードに書き換え |

---

## Phase 5: 完了報告

すべてのファイル生成完了後、以下の形式で報告する：

```
## ✅ セットアップ完了

### 設定された主要情報
| 項目 | 設定値 |
|------|--------|
| 発信者名 | [値] |
| ジャンル | [値] |
| フロント商品 | [値] |
| ミドル商品 | [値] |
| 主要テーマ | [値] |
| inboxサンプル | [あり（X件）/ なし] |

### 作成・更新したファイル（XX件）
[ファイルパス一覧]

### [未定] のまま残った項目
[ある場合のみ記載。後から埋める方法も案内]

### 次のアクション
1. 「戦略を考えたい」→ NOTE_GUNSHI（官兵衛）に壁打ちを依頼
2. 「記事のネタを考えて」→ コンテンツ企画を開始
3. 「今日何するべき？」→ BOSS + GUNSHI がデイリータスクを提案
```

---

## 注意事項

- **必ず上書き**: 既存ファイルに前ユーザーの固有情報（AI系の具体的な言及など）が残っている場合は完全に書き換える
- **inboxは読むだけ**: Phase 3a でサンプルを読み込んだ後、inboxファイル自体は削除・移動しない（ユーザーが判断する）
- **[未定] は残す**: ユーザーが「未定」と答えた項目は `[未定]` プレースホルダーで残し、報告時に案内する
- **スキル変数の確認**: Phase 4 グループI の後に、各スキルで `{...}` が残っていないかチェックし、残っている場合は報告に記載する

$ARGUMENTS
