# OVERSEER 監査基準・構造規約・命名規則

## 監査基準

### 重大度レベル

| レベル | 意味 | 例 |
|--------|------|-----|
| CRITICAL | 機能に影響する問題 | 必須ファイル欠損、参照先が存在しない |
| WARNING | 品質に影響する問題 | 命名規則違反、空ディレクトリ、古いファイル |
| INFO | 軽微な問題 | .DS_Store、不要キャッシュ、微細な不整合 |

### 7つの検出カテゴリ

1. **空ディレクトリ**: 中身のないディレクトリ
2. **重複ファイル**: 同一内容・同一目的のファイル
3. **不要ファイル**: .DS_Store, .gitkeep（中身あり）, *.bak, *.tmp 等
4. **命名規則違反**: 本プロジェクトの命名規約に従わないファイル/ディレクトリ
5. **必須ファイル欠損**: 各エージェントに必要な learnings.md, HISTORY.md 等
6. **孤立ファイル**: どこからも参照されていないファイル
7. **古いファイル**: 90日以上更新のないファイル（workspace/配下）

---

## 構造規約

### プロジェクト標準構造

```
ai-agent-organization/
├── organization/           # エージェント別知識ベース
│   ├── BOSS/               # BOSS（Team Lead）
│   ├── OVERSEER/           # OVERSEER（構造管理）
│   ├── hr-tech/            # ARCHITECT, GENESIS
│   └── operations/         # 実働部隊
├── shared/
│   ├── knowledge/          # 組織共通知識
│   └── templates/          # テンプレート
├── workspace/              # 成果物保存先
└── README.md
```

### 各エージェントの必須ファイル構成

```
[エージェント名]/
├── knowledge/
│   ├── learnings.md        # 学習ログ（必須）
│   └── strategy-brief.md   # 戦略/基準ブリーフ（推奨）
└── HISTORY.md              # 実績履歴（必須）
```

### .claude/ 配下の構造

```
.claude/
├── agents/
│   └── [AGENT_NAME].md     # エージェント定義（大文字スネークケース）
└── skills/
    └── [skill-name]/       # スキルディレクトリ（小文字ケバブケース）
        └── SKILL.md        # スキル定義
```

---

## 命名規則

### ファイル命名

| 対象 | 規則 | 例 |
|------|------|-----|
| エージェントMD | 大文字スネークケース.md | `BOSS.md`, `NOTE_CREATOR.md` |
| スキルディレクトリ | 小文字ケバブケース | `content-review/`, `x-long-post/` |
| knowledge内ファイル | 小文字ケバブケース.md | `learnings.md`, `strategy-brief.md` |
| workspace成果物 | YYYY-MM-DD_type-topic.md | `2026-02-13_article-ai-tools.md` |

### ディレクトリ命名

| 対象 | 規則 | 例 |
|------|------|-----|
| organization配下 | エージェント名またはグループ名 | `BOSS/`, `hr-tech/`, `operations/` |
| skills配下 | 小文字ケバブケース | `directory-audit/`, `health-report/` |

---

## 監査除外対象

以下は監査対象外とする:

- `node_modules/`
- `.git/`
- `*.lock` ファイル
- `.claude/` 配下の設定ファイル（agents/, skills/以外）

---

**変更履歴**:
- 2026-02-13: 初版作成
