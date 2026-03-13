# 新アカウント セットアップガイド

このガイドに従って設定を完了することで、AIエージェント組織をあなたのアカウントに最適化できます。

---

## Step 1: アカウント基本情報

以下を記入してください。

| 項目 | あなたの情報 |
|------|------------|
| Xアカウント名 | @xxx |
| メインテーマ | （例: AI副業・マーケティング・キャリアなど） |
| 発信開始時期 | YYYY年MM月〜 |
| 発信チャネル（使っているもの） | （例: X / note / YouTube / ブログ / メルマガ など） |

---

## Step 2: ターゲット読者・ペルソナ定義

| 項目 | 詳細 |
|------|------|
| メインターゲット（年齢・職業・状況） | （例: 副業初心者の会社員 20-35歳） |
| 読者の抱える課題 | （例: 副業で収益化できない・何から始めればいいか分からない） |
| 読者が求める価値 | （例: すぐに使える具体的なノウハウ・再現性の高い手順） |
| 読者が自分で解決できない理由 | （例: 情報が多すぎてどれが正しいか分からない） |

---

## Step 3: 文体・トーン定義

| 項目 | 詳細 |
|------|------|
| 一人称 | （例: 僕 / 私 / 俺） |
| キャラクター設定 | （例: 年下の専門家 / 同じ目線の先輩 / 実績がある同期） |
| 特徴的な口癖・頻出フレーズ | （例: 「正直に言うと〜」「ここだけの話〜」） |
| NG表現 | （例: 「〜することが重要です」「〜を行いましょう」など硬い表現） |
| 改行スタイル | （例: 1文1行・2-3行で段落など） |

---

## Step 4: 権威性・実績整理

| 項目 | 詳細 |
|------|------|
| 肩書き | （例: 元〇〇のAIエンジニア / 月収XX万達成の副業家） |
| 数値実績 | （例: フォロワーXX人・月収XX万・〇〇人指導） |
| 自己開示エピソード | （読者が共感できる失敗・転機・苦労話） |
| 専門性の根拠 | （学歴・職歴・資格・実績など） |

---

## Step 5: 商品・マネタイズ設計

| 項目 | 詳細 |
|------|------|
| 無料コンテンツの役割 | （例: 信頼構築・認知拡大・リスト獲得） |
| 有料商品①（名称・価格） | （例: 有料記事 1,000-3,000円 / テンプレ販売 / 動画講座 など） |
| 有料商品②（名称・価格） | （例: オンラインコミュニティ 月額3,000-5,000円） |
| 販売プラットフォーム | （例: note / Zenn / Brain / 自前ブログ / Gumroad / ストアカ / 未定） |
| ファネル設計 | （例: 無料X投稿 → 無料記事 → 有料商品 → 継続商品） |
| CTAの置き方 | （例: 記事末尾に自然な形で案内） |

> **注意**: 販売プラットフォームが **note以外** の場合、または **まだ未定** の場合は、
> Step 7 の「エージェント・スキルのリネーム案内」を確認してください。

---

## Step 6: コンテンツテーマ・専門領域

| 項目 | 詳細 |
|------|------|
| 主要テーマ（3-5個） | （例: AI活用・副業収益化・時間短縮術） |
| 絶対に扱わないテーマ | （例: 政治・宗教・特定個人の批判） |
| 競合との差別化ポイント | （例: 再現性の高さ・初心者目線・具体的な手順） |
| あなただけの強み | （例: 業界経験・独自の失敗体験・特殊なスキル） |

---

## Step 7: 設定ファイルへの反映

セットアップ情報を記入したら、以下のファイルに反映してください。

### 反映先ファイル一覧

| ファイル | 反映内容 |
|---------|---------|
| `shared/knowledge/x-note-brand-strategy.md` | 立ち位置・訴求軸・ターゲット・ファネル・商品設計・表現スタイル |
| `note-creator-NOTE_CREATOR/knowledge/knowhow/writing-style-profile.md` | 記事文体・トーン・一人称・自己開示エピソード |
| `x-post-creator-X_POST_CREATOR/knowledge/knowhow/writing-style-profile.md` | X投稿文体・フックパターン・体験入口フレーズ |
| `note-creator-NOTE_CREATOR/knowledge/knowhow/note-operation-guide.md` | 商品URL・CTAリンク |
| `article-reviewer-ARTICLE_REVIEWER/knowledge/knowhow/review-criteria.md` | レビューペルソナ4人の属性・評価視点・商材カテゴリ |
| `data-analyst-DATA_ANALYST/knowledge/knowhow/analysis-methods.md` | Xアカウントのテーマ分類キーワード |

### 新規作成が必要なファイル

以下のファイルは新規作成してください（テンプレートの各ファイルに記載されている箇所に情報を反映）:

1. **creator-achievements.md**（実績ファイル）
   - パス: `organization/operations/note-creator-NOTE_CREATOR/knowledge/knowhow/creator-achievements.md`
   - 内容: Step 4の権威性・実績情報を整理したもの

2. **account-design.md**（アカウント設計ファイル）
   - パス: `organization/operations/gunshi-GUNSHI/knowledge/knowhow/account-design.md`
   - 内容: Step 1-6の情報をまとめた戦略設計書

---

### エージェント・スキルのリネーム案内

このテンプレートはデフォルトで **note** での記事発信・販売を想定した名称になっています。
**noteを使わない場合、または販売プラットフォームが未定の場合** は、以下のリネームを検討してください。

#### リネーム対象

| 現在の名称 | リネーム例（Zennの場合） | リネーム例（ブログの場合） | 内容 |
|-----------|----------------------|------------------------|------|
| `NOTE_CREATOR` エージェント | `ZENN_CREATOR` | `BLOG_CREATOR` | 記事作成エージェント本体 |
| `.claude/agents/NOTE_CREATOR.md` | `ZENN_CREATOR.md` | `BLOG_CREATOR.md` | エージェント定義ファイル |
| `.claude/skills/note-creation/` | `zenn-creation/` | `blog-creation/` | 記事作成スキル |
| `.claude/skills/note-content-planning/` | `content-planning/` | `content-planning/` | コンテンツ企画スキル |
| `.claude/skills/note-strategy-sparring/` | `strategy-sparring/` | `strategy-sparring/` | 戦略壁打ちスキル |
| `.claude/skills/note-competitor-analysis/` | `competitor-analysis/` | `competitor-analysis/` | 競合分析スキル |
| `.claude/skills/note-kpi-pdca/` | `kpi-pdca/` | `kpi-pdca/` | KPI・PDCAスキル |
| `operations/note-creator-NOTE_CREATOR/` | `operations/zenn-creator-ZENN_CREATOR/` | `operations/blog-creator-BLOG_CREATOR/` | エージェント操作ディレクトリ |

#### リネームの判断基準

- **noteを使う確定**: リネーム不要
- **Zenn / ブログ / 他プラットフォームを使う確定**: 対象エージェント・スキルをリネーム
- **まだ未定**: そのままにして、プラットフォームが決まった時点でリネームする

> リネームはGUNSHI（官兵衛）に「エージェントをリネームしたい」と伝えれば、対象ファイルの一括変更を手伝います。

---

## Step 8: 動作確認

設定完了後、以下のコマンドで固有情報が残っていないか確認してください:

```bash
grep -r "\[YOUR_" ai-agent-organization/ --include="*.md" | wc -l
```

プレースホルダー（`[YOUR_XXX]`）がすべて実際の情報に置き換わっていれば設定完了です。

---

## よくある質問

**Q: どのエージェントから使い始めればいい？**
A: まず `GUNSHI`（官兵衛）に「戦略を考えたい」と伝えて、アカウント全体の方向性を固めましょう。どのプラットフォームで何を売るかまだ決まっていなくても大丈夫です。上流から一緒に考えます。

**Q: 記事作成の依頼方法は？**
A: 「note記事を書いて：[テーマ]」と伝えるだけで、`NOTE_CREATOR` → `ARTICLE_STYLIST` が自動連動します。

**Q: X投稿と記事を同時に作りたい場合は？**
A: 「note記事とX投稿を同時に作って：[テーマ]」と伝えると並列処理されます。

---

*このガイドはAIエージェント組織テンプレートの初期設定用ドキュメントです。*
*設定完了後は `SETUP-GUIDE.md` 自体をアーカイブしても構いません。*
