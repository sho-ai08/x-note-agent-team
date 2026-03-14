---
name: setup-org
description: AIエージェント組織を自動構築するスキル。「組織を作りたい」「組織を作って」「セットアップして」などの依頼時に使用。
user-invocable: true
---

# 組織初期化スキル

ユーザーが組織構築を依頼しました。以下の Phase を順番に実行し、組織の全ファイルをそのユーザーに最適化します。

---

## Phase 0: 事前読み込み

以下を読み込んでから開始すること：

1. `ai-agent-organization/system/config.yaml` — 現在の設定値
2. `ai-agent-organization/shared/knowledge/x-note-brand-strategy.md` — 既存の戦略情報（あれば）

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

AskUserQuestion ツールで **Step 1〜6 の各項目を1問ずつ**順番に確認する。

### ルール
- **1項目 = 1回の質問**（複数項目をまとめて聞かない）
- 前の質問への回答を受け取ってから次の質問を投げる
- 「未定」「後で」と答えた項目は `[未定]` プレースホルダーで残す
- 全項目が完了したら次の Step に進む

---

### Step 1: アカウント基本情報

以下の4項目を **1問ずつ**順番に聞く：

1. **Xアカウント名 / ハンドルネーム**（反映先: `[発信者名]`）
   - 例: `@tanaka_ai`

2. **メインテーマ・発信ジャンル**（反映先: `{ジャンル}`）
   - 例: AI副業・マーケティング・キャリアなど

3. **発信開始時期**
   - 例: 2024年4月〜

4. **現在使っている発信チャネル**
   - 例: X / note / YouTube / ブログ / メルマガ など

---

### Step 2: ターゲット読者・ペルソナ定義（関心セグメント）

> **ポイント**: 読者を「習熟度（初心者/中級者）」ではなく**「このテーマを追いかける興味・動機の種類」**で分類してください。
> 例: 「副業で収益化したい人」「仕事の効率化がしたい人」「趣味として楽しみたい人」「キャリアアップしたい人」は
> 経験レベルが同じでも全く異なる読者セグメントです。

以下の4項目を **1問ずつ**順番に聞く：

1. **読者の関心セグメント（3〜5個）**
   - このテーマを追いかける動機・欲求の種類を列挙
   - 例: 「副業収益化」「仕事効率化」「キャリアアップ」「趣味・楽しみ」「コスト削減」

2. **各セグメントの核心動機**
   - 各セグメントが「なぜこのテーマを学ぼうとしているか」を1文で
   - 例: 「副業収益化 → 本業以外の収入源を作って経済的自由を得たい」

3. **各セグメントのペイン（痛み）**
   - 各セグメントが「今まさに困っていること・解決したいこと」

4. **各セグメントの商材への関心**
   - どのセグメントがどの商材に最も関心を持つか

**Step 2 完了後、以下を確認する（1問ずつ）:**
- セグメント数の確認（3〜6個を推奨。多すぎると収拾がつかない）
- 各セグメントに固有のペルソナ名（仮）を決める（例: 「副業タカシ」「効率化アヤカ」）

---

### Step 3: 文体・トーン定義

以下の5項目を **1問ずつ**順番に聞く：

1. **一人称**
   - 例: 僕 / 私 / 俺

2. **キャラクター設定**
   - 例: 年下の専門家 / 同じ目線の先輩 / 実績がある同期

3. **特徴的な口癖・頻出フレーズ**
   - 例: 「正直に言うと〜」「ここだけの話〜」

4. **NG表現**
   - 例: 「〜することが重要です」「〜を行いましょう」など硬い表現

5. **改行スタイル**
   - 例: 1文1行・2-3行で段落など

---

### Step 4: 権威性・実績整理

以下の4項目を **1問ずつ**順番に聞く：

1. **肩書き**
   - 例: 元〇〇のAIエンジニア / 月収XX万達成の副業家

2. **数値実績**（反映先: `{発信者の強み②}`）
   - 例: フォロワーXX人・月収XX万・〇〇人指導

3. **自己開示エピソード**
   - 読者が共感できる失敗・転機・苦労話

4. **専門性の根拠**（反映先: `{発信者の強み①}`）
   - 学歴・職歴・資格・実績など

---

### Step 5: 商品・マネタイズ設計

以下の6項目を **1問ずつ**順番に聞く：

1. **無料コンテンツの役割**
   - 例: 信頼構築・認知拡大・リスト獲得

2. **有料商品①（名称・価格）**（反映先: `{フロント商品}`）
   - 例: 有料記事 1,000-3,000円 / テンプレ販売 / 動画講座

3. **有料商品②（名称・価格）**（反映先: `{ミドル商品}` `{サロン名}`）
   - 例: オンラインコミュニティ 月額3,000-5,000円

4. **販売プラットフォーム** ← **重要**: 後のリネーム判断に使用
   - 例: note / Zenn / Brain / 自前ブログ / Gumroad / ストアカ / **未定**

5. **ファネル設計**
   - 例: 無料X投稿 → 無料記事 → 有料商品 → 継続商品

6. **CTAの置き方**
   - 例: 記事末尾に自然な形で案内

---

### Step 6: コンテンツテーマ・専門領域

以下の4項目を **1問ずつ**順番に聞く：

1. **主要テーマ（3-5個）**（反映先: `{テーマタグ①②}`）
   - 例: AI活用・副業収益化・時間短縮術

2. **絶対に扱わないテーマ**
   - 例: 政治・宗教・特定個人の批判

3. **競合との差別化ポイント**（反映先: `{発信者の強み③}`）
   - 例: 再現性の高さ・初心者目線・具体的な手順

4. **あなただけの強み**
   - 例: 業界経験・独自の失敗体験・特殊なスキル

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

| ファイルパス | 反映内容 | 参照ステップ |
|------------|---------|------------|
| `ai-agent-organization/shared/knowledge/x-note-brand-strategy.md` | 立ち位置・訴求軸・ターゲット・ファネル・商品設計・表現スタイル | Step 1〜6 全体 |
| `ai-agent-organization/system/config.yaml` | `project.owner`（発信者名）・`project.description`（ジャンル・目的） | Step 1 |

---

### グループB: BOSS ナレッジ

| ファイルパス | 反映内容 | 参照ステップ |
|------------|---------|------------|
| `ai-agent-organization/organization/BOSS/knowledge/knowhow/strategy-brief.md` | ターゲット・商品ライン・ファネル設計・発信者の強み | Step 2・4・5・6 |
| `ai-agent-organization/organization/BOSS/knowledge/knowhow/strategy-overview.md` | 全体戦略の概要・フェーズ・KPI目標 | Step 5・6 |

---

### グループC: note記事作成エージェント（NOTE_CREATOR）

| ファイルパス | 反映内容 | 参照ステップ |
|------------|---------|------------|
| `ai-agent-organization/organization/operations/note-creator-NOTE_CREATOR/knowledge/knowhow/writing-style-profile.md` | 一人称・トーン・口癖・NG表現・文章設計思想 | Step 3・4 + inboxサンプル |
| `ai-agent-organization/organization/operations/note-creator-NOTE_CREATOR/knowledge/knowhow/sentence-ending-patterns.md` | 語尾パターン一覧 | Step 3 + inboxサンプル |
| `ai-agent-organization/organization/operations/note-creator-NOTE_CREATOR/knowledge/knowhow/article-creation-process.md` | 記事作成フロー・対象テーマ・商品連動CTAの設計 | Step 5・6 |
| `ai-agent-organization/organization/operations/note-creator-NOTE_CREATOR/knowledge/knowhow/creator-achievements.md` | 権威性・実績まとめ **【新規作成】** | Step 4 |

---

### グループD: X投稿作成エージェント（X_POST_CREATOR）

| ファイルパス | 反映内容 | 参照ステップ |
|------------|---------|------------|
| `ai-agent-organization/organization/operations/x-post-creator-X_POST_CREATOR/knowledge/knowhow/writing-style-profile.md` | X投稿の文体・フックパターン・体験入口フレーズ | Step 3・4 + inboxサンプル |
| `ai-agent-organization/organization/operations/x-post-creator-X_POST_CREATOR/knowledge/knowhow/sentence-ending-patterns.md` | X投稿で使う語尾パターン | Step 3 + inboxサンプル |
| `ai-agent-organization/organization/operations/x-post-creator-X_POST_CREATOR/knowledge/knowhow/x-post-best-practices.md` | 発信ベストプラクティス・テーマ別フックパターン | Step 6 + inboxサンプル |

---

### グループE: 記事レビューエージェント（ARTICLE_REVIEWER）

ペルソナ定義はknowledgeの個別ファイルに分離されています。
**Step 2で特定した関心セグメントの数だけ**、ペルソナファイルを新規作成してください。

#### ペルソナファイルの作成ルール

1. **既存のスケルトンファイルは参考テンプレートとして使用する**
   - `persona-01-problem-solver.md`（即課題解決型のテンプレート）
   - `persona-02-skill-investor.md`（スキル投資・成長型のテンプレート）
   - `persona-03-community-seeker.md`（つながり・共感型のテンプレート）
   - `persona-04-roi-optimizer.md`（ROI最適化型のテンプレート）

2. **実際に作成するファイルは、Step 2で特定したセグメントに対応した内容に**
   - ファイル名は `persona-NN-[セグメント識別名].md` の形式（例: `persona-01-side-hustle.md`, `persona-02-work-efficiency.md`）
   - セグメントのタイプに最も近いスケルトンを参考にして作成
   - **スケルトンファイル自体は削除しない**（別のユーザーがテンプレートとして使えるよう保持）

3. **各ペルソナファイルに必ず含める内容:**

| セクション | 反映内容 | 参照ステップ |
|-----------|---------|------------|
| `## 興味・関心の核心` | このセグメントがコンテンツを探す根本動機（1〜2文） | Step 2 |
| `## プロフィール` | 名前（仮）・年齢・職業・テーマとの関わり方・核心動機・商材関心 | Step 2・5 |
| `## このペルソナの内面` | 3つの内なる声（このセグメント固有の思考・感情） | Step 2 |
| `## 「刺さる」コンテンツの特徴` | このセグメントの興味・動機に響く切り口3つ | Step 2・6 |
| `## 媒体別の評価背景` | X閲覧時・note閲覧時の具体的な行動・感情 | Step 2・6 |
| `## 評価の思考回路` | このセグメントの興味軸に沿った4ステップ評価フロー | Step 2 |
| `## スコアリング基準` | コンテンツ価値6割・商材関心4割のスコア定義 | Step 2・5 |
| `## 関連記事提案の視点` | 前提記事・次記事・商材への導線 | Step 5 |

---

### グループF: 記事装飾エージェント（ARTICLE_STYLIST）

| ファイルパス | 反映内容 | 参照ステップ |
|------------|---------|------------|
| `ai-agent-organization/organization/operations/article-stylist-ARTICLE_STYLIST/knowledge/knowhow/styling-guidelines.md` | 装飾スタイル・ハッシュタグ方針・有料記事への誘導デザイン | Step 3・5 |
| `ai-agent-organization/organization/operations/article-stylist-ARTICLE_STYLIST/knowledge/knowhow/cta-and-navigation.md` | CTA文言・商品URL・関連記事導線 | Step 5 |

---

### グループG: データ分析エージェント（DATA_ANALYST）

| ファイルパス | 反映内容 | 参照ステップ |
|------------|---------|------------|
| `ai-agent-organization/organization/operations/data-analyst-DATA_ANALYST/knowledge/knowhow/analysis-methods.md` | Xアカウントのテーマ分類キーワード（`[YOUR_THEME_*]` を実際の値で記載） | Step 6 + inboxサンプル |

---

### グループH: 戦略参謀エージェント（GUNSHI）

| ファイルパス | 反映内容 | 参照ステップ |
|------------|---------|------------|
| `ai-agent-organization/organization/operations/gunshi-GUNSHI/knowledge/knowhow/account-design.md` | Step 1〜6 の情報をまとめた戦略設計書 **【新規作成】** | Step 1〜6 全体 |
| `ai-agent-organization/organization/operations/gunshi-GUNSHI/knowledge/knowhow/master-strategy.md` | コンテンツ戦略・KPI・商品ラインの全体設計（未定項目は `[未定]` プレースホルダーで残す） **【新規作成】** | Step 2・5・6 |

---

### グループI: スキルファイルへの変数反映

成果物系スキルの `{...}` 変数を実際の値に書き換える。**inboxのサンプルがある場合は精緻化、ない場合はヒアリング値で埋める**。

| スキルファイルパス | 更新対象の変数・セクション | 参照ステップ |
|-----------------|------------------------|------------|
| `.claude/skills/x-long-post/SKILL.md` | `実演型コンテンツのフォーマット` 内のAI固有例を `{ジャンル}` に合わせた例に書き換え | Step 6 |
| `.claude/skills/note-content-planning/SKILL.md` | `{フロント商品}` `{ミドル商品}` を実際の商品名・価格に書き換え | Step 5 |
| `.claude/skills/note-strategy-sparring/SKILL.md` | `{フロント商品}` `{ミドル商品}` を実際の商品名・価格に書き換え | Step 5 |
| `.claude/skills/note-competitor-analysis/SKILL.md` | `{ジャンル}` `{発信者の強み①②③}` を実際の値に書き換え | Step 4・6 |
| `.claude/skills/x-analytics-analysis/SKILL.md` | `{テーマタグ①②}` を実際のテーマキーワードに書き換え | Step 6 |
| `.claude/skills/daily-strategy/SKILL.md` | ユーザーコンテキスト参照先の knowledge ファイルパスを確認・修正 | Step 1 |

---

### エージェント定義ファイル（`.claude/agents/*.md`）について

`.claude/agents/` 配下のエージェント定義ファイル自体（`NOTE_CREATOR.md` 等）は**基本的に編集不要**。
各エージェントはタスク実行時に `knowledge/` ファイルを動的に参照するため、グループC〜H の knowledge ファイルを更新すれば自動的に反映される。

ただし以下の場合はエージェント定義ファイルも編集が必要：

| 変更ケース | 編集対象ファイル |
|-----------|----------------|
| エージェントの人格・口調を根本的に変えたい | `.claude/agents/[AGENT_NAME].md` の「人格・口調」セクション |
| エージェントが参照するスキルを追加・変更したい | `.claude/agents/[AGENT_NAME].md` の `skills:` フロントマター |
| プラットフォームリネームを行った場合 | リネーム後の `[NEW_NAME].md` を新規作成し、旧ファイルを削除 |

---

## Phase 4.5: リネーム案内（販売プラットフォームが note 以外 or 未定の場合）

Step 5 でヒアリングした「販売プラットフォーム」を確認し、以下の判定を行う：

- **noteを使う（確定）**: リネーム不要。Phase 5 へ進む
- **note以外のプラットフォームを使う**: 以下のリネーム案内をユーザーに提示する
- **未定**: 以下のリネーム案内をユーザーに提示する（今はリネームしなくてよい旨も伝える）

### リネーム対象

| 現在の名称 | リネーム例（Zennの場合） | リネーム例（ブログの場合） |
|-----------|----------------------|------------------------|
| `NOTE_CREATOR` エージェント | `ZENN_CREATOR` | `BLOG_CREATOR` |
| `.claude/agents/NOTE_CREATOR.md` | `ZENN_CREATOR.md` | `BLOG_CREATOR.md` |
| `.claude/skills/note-creation/` | `zenn-creation/` | `blog-creation/` |
| `.claude/skills/note-content-planning/` | `content-planning/` | `content-planning/` |
| `.claude/skills/note-strategy-sparring/` | `strategy-sparring/` | `strategy-sparring/` |
| `.claude/skills/note-competitor-analysis/` | `competitor-analysis/` | `competitor-analysis/` |
| `.claude/skills/note-kpi-pdca/` | `kpi-pdca/` | `kpi-pdca/` |
| `operations/note-creator-NOTE_CREATOR/` | `operations/zenn-creator-ZENN_CREATOR/` | `operations/blog-creator-BLOG_CREATOR/` |

> リネームは GUNSHI（官兵衛）に「エージェントをリネームしたい」と伝えれば一括変更を手伝います。

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
| 販売プラットフォーム | [値 or 未定] |
| フロント商品 | [値 or 未定] |
| ミドル商品 | [値 or 未定] |
| 主要テーマ | [値] |
| inboxサンプル | [あり（X件）/ なし] |

### 作成・更新したファイル（XX件）
[ファイルパス一覧]

### [未定] のまま残った項目
[ある場合のみ記載。後から埋める方法も案内]

### エージェント・スキルのリネーム
[noteを使う確定の場合: 「リネーム不要」]
[note以外 or 未定の場合: 「プラットフォーム確定後にGUNSHIへリネーム依頼を」と案内]

### 動作確認
以下のコマンドでプレースホルダーが残っていないか確認できます:
\`\`\`bash
grep -r "\[YOUR_" ai-agent-organization/ --include="*.md" | wc -l
\`\`\`
0件であれば設定完了です。

### 次のアクション
1. 「戦略を考えたい」→ GUNSHI（官兵衛）に壁打ちを依頼（プラットフォーム未定でもOK）
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
