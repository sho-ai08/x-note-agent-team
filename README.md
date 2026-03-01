# AI Agent Organization Template

**ライセンス**: MIT

「〜の組織を作って」と指示するだけで、AIエージェント組織が自動構築されるテンプレート

---

## 概要

AI Agent Organization Templateは、**あなただけのAIエージェント組織**を構築するためのテンプレートです。

「〇〇をする組織を作って」と指示するだけで、SOVEREIGNが組織の初期化を実行し、GENESISが必要なエージェントを自動作成します。

### 初期状態

テンプレートにはコアエージェント5体のみが含まれます：

| エージェント | コードネーム | 役割 |
|------------|------------|------|
| CEO | SOVEREIGN | 組織統括、組織初期化、タスクルーティング |
| Director | BOSS | 実働部隊統括、タスク分解 |
| Agent Designer | GENESIS | エージェント設計・作成 |
| Prompt Engineer | ARCHITECT | プロンプト作成・改善 |
| Agent Trainer | MENTOR | フィードバック解析・経験値付与 |

**operations/** 配下は空で、ユーザーの依頼に応じて実働エージェントが動的に作成されます。

### 特徴

- **自動初期化**: 「〜の組織を作って」で組織が自動構築
- **自己拡張**: 必要に応じて新しいエージェントを自動作成
- **学習機能**: フィードバックを蓄積し、エージェントが成長
- **柔軟性**: どんな領域の組織でも構築可能
- **Claude Code統合**: Claude Codeと連携してタスクを自動実行

---

## クイックスタート

### 1. テンプレートをクローン

```bash
# このリポジトリをforkまたはクローンしてください
git clone <your-repository-url>
cd ai-agent-organization-template
```

### 2. 組織を自動構築（推奨）

Claude Codeで以下を実行：

```bash
claude "カスタマーサポート業務を行う組織を作って"
```

**SOVEREIGNが自動で実行する処理:**
1. ユーザーにヒアリング（組織の目標・専門領域を確認）
2. `shared/knowledge/` 配下のファイルを自動入力
3. GENESISを起動して必要なエージェントを作成

### 3. タスクを実行

```bash
claude "お客様からの問い合わせに返信して"
```

作成されたエージェントがタスクを実行します。

### 手動セットアップ（オプション）

自動初期化を使わず手動でセットアップすることも可能です：

1. `ai-agent-organization/system/config.yaml` を編集
2. `ai-agent-organization/shared/knowledge/` 配下のファイルを編集
   - `organization-goals.md` - 組織の目標・ミッション
   - `domain-knowledge.md` - 専門領域の知識
   - `guidelines.md` - 品質基準・ガイドライン
3. 必要に応じてエージェントを作成

詳細は [QUICKSTART.md](./QUICKSTART.md) を参照してください。

---

## プロジェクト構成

```
ai-agent-organization-template/
├── README.md                      # このファイル
├── QUICKSTART.md                  # クイックスタートガイド
├── LICENSE                        # MITライセンス
│
├── .claude/agents/                # Claude Code用エージェント設定
│   ├── SOVEREIGN.md              # CEO
│   ├── BOSS.md                   # ディレクター
│   ├── GENESIS.md                # エージェントデザイナー
│   ├── ARCHITECT.md              # プロンプトエンジニア
│   └── MENTOR.md                 # エージェントトレーナー
│
├── ai-agent-organization/         # エージェント組織本体
│   ├── organization/              # エージェント配置
│   │   ├── executive/            # 経営層（SOVEREIGN, BOSS）
│   │   ├── hr-tech/              # HR-Tech（GENESIS, ARCHITECT）
│   │   └── operations/           # 実働部隊（動的に追加）
│   │
│   ├── shared/                    # 共有リソース
│   │   ├── knowledge/            # 組織共通の知識
│   │   └── templates/            # テンプレート
│   │
│   ├── system/                    # システム設定
│   │   ├── config.yaml           # 組織設定
│   │   ├── routing-rules.yaml    # ルーティングルール
│   │   ├── auto-expansion-rules.yaml # 自動拡張ルール
│   │   ├── skills.yaml           # スキル定義
│   │   └── growth-system.yaml    # 成長システム
│   │
│   ├── workspace/                 # 成果物保存先
│   └── ROUTING.md                 # ルーティング詳細
│
└── dashboard/                     # Webダッシュボード（オプション）
    └── ...
```

---

## コアエージェント

テンプレートには5体のコアエージェントのみが含まれています（初期状態）。

| エージェント | コードネーム | 役割 |
|------------|------------|------|
| **CEO** | SOVEREIGN | 組織全体の統括、**組織初期化**、タスクルーティング、戦略的判断 |
| **ディレクター** | BOSS | 実働部隊の統括、タスク分解、品質管理 |
| **エージェントデザイナー** | GENESIS | 新規エージェントの設計・作成、設定ファイル自動更新 |
| **プロンプトエンジニア** | ARCHITECT | プロンプトの作成・改善・テスト |
| **エージェントトレーナー** | MENTOR | フィードバック解析・経験値付与・育成 |

### 動的エージェント

**初期状態**: `organization/operations/` は空のディレクトリです。

ユーザーの依頼に応じてGENESISがエージェントを作成し、自動的にルーティングシステムに統合されます。

| 依頼例 | 作成されるエージェント |
|-------|---------------------|
| 「技術記事を書くエージェントを作って」 | TECH-WRITER |
| 「カスタマーサポートエージェントを作って」 | CS-SPECIALIST |
| 「SNS投稿を作成するエージェントを作って」 | SOCIAL |

---

## 使用例

### 技術ブログ組織

```bash
claude "技術ブログを書く組織を作りたい"
# → TECH-WRITERエージェントが自動作成される

claude "Reactのカスタムフックについて記事を書いて"
# → TECH-WRITERが記事を作成
```

### カスタマーサポート組織

```bash
claude "カスタマーサポートをする組織を作りたい"
# → CS-SPECIALISTエージェントが自動作成される

claude "お客様からの問い合わせに返信して"
# → CS-SPECIALISTが返信を作成
```

### マーケティング組織

```bash
claude "マーケティング戦略を立案する組織を作りたい"
# → MARKETING-PLANNERエージェントが自動作成される

claude "新製品のマーケティング計画を立てて"
# → MARKETING-PLANNERが計画を作成
```

---

## 組織の成長

タスクをこなすほど組織は成長します。

### 成長の仕組み

1. **経験値獲得**: タスク完了時に経験値を獲得
2. **レベルアップ**: 経験値が一定量に達するとレベルアップ
3. **スキル向上**: 関連スキルのポイントが増加
4. **学びの蓄積**: フィードバックがlearnings.mdに記録
5. **プロンプト改善**: ARCHITECTが学びをプロンプトに反映

### レベル帯

| レベル | 称号 |
|--------|------|
| 1-5 | 見習い |
| 6-10 | 一人前 |
| 11-15 | 熟練 |
| 16-20 | エキスパート |
| 21-30 | マスター |
| 31-50 | グランドマスター |
| 51-100 | レジェンド |

---

## ダッシュボード（オプション）

Webダッシュボードでエージェントの状態を可視化できます。

### セットアップ

```bash
cd dashboard
npm install
npm run dev
```

ブラウザで http://localhost:3000 を開く

### 機能

- エージェント一覧・詳細表示
- ステータス・スキルの可視化
- 組織構成図
- 成果物の管理

---

## 技術仕様

### 前提条件

- Node.js 18以上（ダッシュボード使用時）
- Claude Code CLI

### データ形式

- **設定ファイル**: YAML
- **エージェント定義**: Markdown
- **成果物**: Markdown

### Claude Code統合

`.claude/agents/` 配下のファイルがClaude Codeに読み込まれ、タスクの自動ルーティングとエージェント起動が行われます。

---

## カスタマイズ

### 組織目標の設定

`shared/knowledge/organization-goals.md` を編集してミッション・ビジョン・バリューを定義:

```markdown
## ミッション
[あなたの組織のミッション]

## ビジョン
[組織が目指す将来像]

## コアバリュー
1. [価値観1]
2. [価値観2]
```

### ドメイン知識の追加

`shared/knowledge/domain-knowledge.md` に専門知識を記載:

```markdown
## 専門領域
- [領域1]
- [領域2]

## 重要な概念
### [概念名]
[概念の説明]
```

### 品質基準の定義

`shared/knowledge/guidelines.md` で品質基準を設定:

```markdown
## 品質基準
- [ ] [基準1]
- [ ] [基準2]

## 避けるべきこと
- [避けること1]
- [避けること2]
```

---

## ライセンス

MIT License - 詳細は [LICENSE](./LICENSE) を参照

---

## 貢献

Issue や Pull Request を歓迎します。

---

## 関連リンク

- [QUICKSTART.md](./QUICKSTART.md) - 詳細なクイックスタートガイド
- [ROUTING.md](./ai-agent-organization/ROUTING.md) - タスクルーティングの詳細
- [Claude Code](https://claude.ai) - Anthropic公式CLI

---

**Powered by Claude Code**
