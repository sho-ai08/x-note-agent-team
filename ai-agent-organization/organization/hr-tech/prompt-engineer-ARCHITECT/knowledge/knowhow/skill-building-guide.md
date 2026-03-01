# Claude スキル構築完全ガイド

## 概要

Anthropic公式ドキュメント「The Complete Guide to Building Skills for Claude」の要点整理。
スキル（SKILL.md）を設計・作成する際の技術的要件、設計原則、テスト手法をまとめたノウハウ集。

**出典**: The Complete Guide to Building Skills for Claude（Anthropic公式, 2026年1月時点）

---

## 1. スキルの基礎知識

### 1.1 スキルとは

スキルは**フォルダ**として構成されるClaudeへの指示パッケージ。一度教えれば毎回活用できる。

```
your-skill-name/
├── SKILL.md          # 必須：メインの指示ファイル
├── scripts/          # オプション：実行可能コード（Python, Bash等）
├── references/       # オプション：参照ドキュメント
└── assets/           # オプション：テンプレート、フォント、アイコン等
```

### 1.2 スキルが有効な場面

- 繰り返し発生するワークフロー（フロントエンド設計、リサーチ、ドキュメント生成）
- 一貫した方法論が必要なマルチステップ処理
- チームのスタイルガイドに沿った成果物作成
- MCPとの組み合わせによるツールアクセスの自動化

### 1.3 3つのコア設計原則

#### Progressive Disclosure（段階的開示）
3レベルのコンテキスト管理でトークン消費を最小化：

| レベル | 内容 | タイミング |
|--------|------|-----------|
| Level 1 | YAMLフロントマター | 常にシステムプロンプトに読み込み |
| Level 2 | SKILL.md本文 | スキルが関連すると判断した時 |
| Level 3 | リンクされたファイル | Claudeが必要と判断した時のみ |

#### Composability（組み合わせ可能性）
- 複数のスキルを同時に読み込める設計
- 他のスキルが存在することを前提とした設計

#### Portability（移植性）
- Claude.ai、Claude Code、API で同一動作
- 一度作成すれば全サーフェスで利用可能

---

## 2. 技術的要件

### 2.1 ファイル命名ルール

**SKILL.md の命名：**
- 必ず `SKILL.md`（大文字・小文字厳守）
- `SKILL.MD`、`skill.md` などは無効

**フォルダの命名：**
```
✅ 正しい: notion-project-setup
❌ 誤り:   Notion Project Setup（スペース）
❌ 誤り:   notion_project_setup（アンダースコア）
❌ 誤り:   NotionProjectSetup（キャメルケース）
```

**README.mdは含めない：**
- スキルフォルダ内にREADME.mdを入れない
- ドキュメントはSKILL.mdまたはreferences/に記載

### 2.2 YAMLフロントマター（最重要）

YAMLフロントマターはClaudeがスキルを読み込むかどうかを判断する根拠。

**最小構成：**
```yaml
---
name: your-skill-name
description: What it does. Use when user asks to [specific phrases].
---
```

**全フィールド：**
```yaml
---
name: skill-name                    # 必須: kebab-case
description: 説明文                  # 必須: 1024文字以内
license: MIT                        # オプション: OSSライセンス
compatibility: Claude Code required # オプション: 1-500文字
metadata:                           # オプション: カスタムフィールド
  author: CompanyName
  version: 1.0.0
  mcp-server: server-name
  category: productivity
---
```

**セキュリティ制限（絶対禁止）：**
- XMLアングルブラケット（`<` `>`）
- name に "claude" または "anthropic" を含む（予約済み）

### 2.3 descriptionフィールドの書き方

**構造：** `[何をするか] + [いつ使うか] + [主要な機能]`

```yaml
# ✅ 良い例：具体的でトリガーフレーズ含む
description: Analyzes Figma design files and generates developer
  handoff documentation. Use when user uploads .fig files, asks
  for "design specs", "component documentation", or
  "design-to-code handoff".

# ❌ 悪い例：漠然としすぎ
description: Helps with projects.

# ❌ 悪い例：トリガーがない
description: Creates sophisticated multi-page documentation systems.
```

---

## 3. ユースケースカテゴリ

Anthropicが観察した3つの代表的ユースケース：

### Category 1: Document & Asset Creation
**用途**: ドキュメント、プレゼン、アプリ、デザイン等の一貫した高品質成果物

**主要テクニック:**
- 埋め込まれたスタイルガイド・ブランド基準
- 一貫した出力のためのテンプレート構造
- 最終化前のクオリティチェックリスト
- 外部ツール不要（Claudeのネイティブ機能のみ使用）

### Category 2: Workflow Automation
**用途**: 一貫した方法論が必要なマルチステップ処理、複数MCPサーバーの調整

**主要テクニック:**
- バリデーションゲート付きのステップバイステップワークフロー
- 共通構造のテンプレート
- 内蔵レビューと改善提案
- 反復的な改善ループ

### Category 3: MCP Enhancement
**用途**: MCPサーバーが提供するツールアクセスにワークフロー知識を追加

**主要テクニック:**
- 複数のMCPコールを順次調整
- ドメイン知識の組み込み
- ユーザーが指定しなくてもコンテキストを提供
- MCPよくある問題のエラーハンドリング

---

## 4. スキル設計のベストプラクティス

### 4.1 指示の書き方

**推奨構造：**
```markdown
---
name: your-skill
description: [...]
---

# Your Skill Name

## Instructions

### Step 1: [最初のステップ]
何が起きるかの明確な説明。

Example:
```bash
python scripts/fetch_data.py --project-id PROJECT_ID
Expected output: [成功時の状態]
```

## Examples

### Example 1: [一般的なシナリオ]
User says: "..."
Actions:
1. ...
2. ...
Result: ...

## Troubleshooting

### Error: [よくあるエラー]
Cause: [原因]
Solution: [解決策]
```

**具体的・実行可能にする：**
```
✅ 良い: Run `python scripts/validate.py --input {filename}` to check data format.
❌ 悪い: Validate the data before proceeding.
```

**エラーハンドリングを含める：**
```markdown
## Common Issues

### MCP Connection Failed
If you see "Connection refused":
1. Verify MCP server is running
2. Confirm API key is valid
3. Try reconnecting
```

### 4.2 Progressive Disclosureの実践

- SKILL.mdはコア指示に集中
- 詳細ドキュメントは `references/` に移動してリンク
- SKILL.mdは**5,000語以内**を目標

### 4.3 MCPとスキルの組み合わせ（台所の比喩）

| MCP（プロフェッショナルキッチン） | スキル（レシピ） |
|--------------------------------|----------------|
| ツール・食材・設備へのアクセス提供 | 価値あるものを作る手順を提供 |
| Claudeが「何を」できるか | Claudeが「どのように」すべきか |
| リアルタイムデータアクセス | ワークフローとベストプラクティス |

---

## 5. テストと改善

### 5.1 テストレベル

- **手動テスト（Claude.ai）**: クエリを直接実行、高速な反復
- **スクリプトテスト（Claude Code）**: 変更を跨いだ繰り返し検証の自動化
- **プログラマティックテスト（Skills API）**: 体系的な評価スイート構築

**Pro Tip**: まず単一の難しいタスクを反復して成功させ、そのアプローチをスキル化する。

### 5.2 推奨テスト項目

**1. トリガーテスト（最重要）**
```
# トリガーすべきケース
- "Help me set up a new workspace"
- "I need to create a project"      # 言い換えでも動作するか
- "Initialize a project for Q4"

# トリガーすべきでないケース
- "What's the weather in San Francisco?"
- "Help me write Python code"
```

**2. 機能テスト**
```
Test: Create project with 5 tasks
Given: Project name "Q4 Planning", 5 task descriptions
When: Skill executes workflow
Then:
  - Project created
  - 5 tasks created with correct properties
  - No API errors
```

**3. パフォーマンス比較**
```
Without skill: 15 back-and-forth messages, 12,000 tokens consumed
With skill: 2 clarifying questions only, 6,000 tokens consumed
```

### 5.3 成功基準

**定量指標:**
- 関連クエリの90%でスキルが自動トリガー
- 1ワークフロー当たりのAPIコール失敗0件

**定性指標:**
- ユーザーが次のステップをClaudeに促す必要がない
- ユーザーの訂正なしにワークフロー完了
- セッションをまたいで一貫した結果

### 5.4 トリガー調整の方法

| 症状 | 原因 | 解決策 |
|------|------|--------|
| スキルが全然トリガーされない（Under-triggering） | descriptionが曖昧すぎる | 具体的なキーワード・フレーズを追加 |
| 無関係なクエリでトリガーされる（Over-triggering） | descriptionが広すぎる | ネガティブトリガーを追加、スコープを限定 |
| 指示が守られない | 指示が長すぎる/埋もれている | 箇条書き化、重要事項を先頭に |

---

## 6. ワークフローパターン集

### Pattern 1: Sequential Workflow Orchestration
**用途**: 特定の順序でマルチステップ処理が必要な場合

```markdown
## Workflow: Onboard New Customer

### Step 1: Create Account
Call MCP tool: `create_customer`
Parameters: name, email, company

### Step 2: Setup Payment
Call MCP tool: `setup_payment_method`
Wait for: payment method verification

### Step 3: Send Welcome Email
Call MCP tool: `send_email`
Template: welcome_email_template
```

**キーテクニック:** 明示的なステップ順序、ステップ間の依存関係、各段階でのバリデーション、失敗時のロールバック

### Pattern 2: Multi-MCP Coordination
**用途**: 複数サービスにまたがるワークフロー

```markdown
## Phase 1: Design Export (Figma MCP)
## Phase 2: Asset Storage (Drive MCP)
## Phase 3: Task Creation (Linear MCP)
## Phase 4: Notification (Slack MCP)
```

**キーテクニック:** 明確なフェーズ分離、MCP間のデータ引き渡し、次フェーズ移行前のバリデーション

### Pattern 3: Iterative Refinement
**用途**: 反復によって出力品質が向上する場合

```markdown
## Initial Draft → Quality Check → Refinement Loop → Finalization
```

**キーテクニック:** 明示的な品質基準、検証スクリプト、反復停止条件

### Pattern 4: Context-aware Tool Selection
**用途**: 同じ結果を、コンテキストによって異なるツールで実現する場合

```markdown
## Decision Tree
1. Check file type and size
2. Determine best storage:
   - Large files (>10MB): cloud storage MCP
   - Collaborative docs: Notion/Docs MCP
   - Code files: GitHub MCP
```

### Pattern 5: Domain-specific Intelligence
**用途**: ツールアクセスを超えた専門知識をスキルに埋め込む場合

**キーテクニック:** ロジックに専門知識を組み込む、アクション前のコンプライアンスチェック、包括的な記録

---

## 7. トラブルシューティング早見表

### スキルがアップロードできない

| エラー | 原因 | 解決策 |
|--------|------|--------|
| "Could not find SKILL.md" | ファイル名が違う | 必ず `SKILL.md`（大文字小文字厳守） |
| "Invalid frontmatter" | YAMLの区切り文字がない | `---` で挟む |
| "Invalid skill name" | nameにスペースや大文字 | kebab-caseのみ |

**YAMLの正しい書き方：**
```yaml
# ❌ Wrong - delimiters missing
name: my-skill
description: Does things

# ✅ Correct
---
name: my-skill
description: Does things
---
```

### MCPコネクション問題

```
チェックリスト:
1. MCPサーバーが起動しているか確認
2. 認証情報（APIキー）が有効か確認
3. MCPを単独でテスト（スキルなしで直接呼び出す）
4. ツール名のスペルが正確か確認（大文字小文字区別あり）
```

### 指示が守られない

```markdown
## ❌ 曖昧な指示
Make sure to validate things properly

## ✅ 明確な指示
CRITICAL: Before calling create_project, verify:
- Project name is non-empty
- At least one team member assigned
- Start date is not in the past
```

**上級テクニック**: 重要なバリデーションはスクリプト化（言語指示より確実）

### コンテキストサイズ問題

- SKILL.mdを5,000語以内に
- 詳細なドキュメントは `references/` に移動
- 同時に有効化するスキルは20〜50以下が目安

---

## 8. クイックチェックリスト

### 開発中
- [ ] フォルダ名がkebab-case
- [ ] `SKILL.md`が存在する（大文字小文字厳守）
- [ ] YAMLフロントマターに `---` 区切り
- [ ] `name`フィールドがkebab-case
- [ ] `description`に「何をするか」と「いつ使うか」の両方
- [ ] XMLタグ（`<` `>`）が含まれていない
- [ ] 指示が具体的・実行可能
- [ ] エラーハンドリングが含まれている
- [ ] 使用例が提供されている

### アップロード前
- [ ] 明示的なクエリでトリガーされるか確認
- [ ] 言い換えクエリでもトリガーされるか確認
- [ ] 無関係なクエリでトリガーされないか確認
- [ ] 機能テストが通過するか確認

### アップロード後
- [ ] 実際の会話でテスト
- [ ] Under/Over-triggeringを監視
- [ ] ユーザーフィードバックを収集
- [ ] descriptionと指示を反復改善

---

## 変更履歴

| バージョン | 日付 | 変更内容 |
|-----------|------|---------|
| 1.0.0 | 2026-02-18 | 初版作成（Anthropic公式ガイドより要点整理） |

---

## 関連ファイル

- [prompt-engineering-principles.md](prompt-engineering-principles.md) - プロンプト設計の基本原則
- [prompt-patterns.md](prompt-patterns.md) - プロンプトパターン集
- ARCHITECT エージェントMD（`.claude/agents/ARCHITECT.md`）
