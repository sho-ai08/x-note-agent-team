---
name: daily-strategy
description: 副業戦略ロードマップに基づき、今日・今週やるべきことを BOSSとGUNSHIが連携して提案するスキル。「今日何するべき」「今週のタスクは」「何から始める」「今何をすべきか」などのキーワードで自動起動。
---

# daily-strategy スキル

## 目的

副業戦略ロードマップと現在地を照合し、
今日・今週に取り組むべき具体的なアクションをBOSSとGUNSHIが連携して提案する。

---

## 実行フロー

### Step 1: 現状把握（BOSSが実行）

以下のファイルを確認する：

1. `ai-agent-organization/organization/BOSS/knowledge/knowhow/business-strategy-2025-2026.md`
   → 月次ロードマップで現フェーズを特定
   → 優先アクション・残課題を確認

2. `ai-agent-organization/organization/BOSS/knowledge/knowhow/strategy-brief.md`
   → 中長期の方向性とファネル全体図を確認

3. `ai-agent-organization/organization/operations/note-gunshi-NOTE_GUNSHI/knowledge/knowhow/master-strategy.md`
   → コンテンツ戦略・KPI・商品ラインとの整合性確認

4. `ai-agent-organization/organization/BOSS/learnings.md`
   → 過去の学び（weight 5以上は最優先）

---

### Step 2: GUNSHIへの確認（Task tool でNOTE_GUNSHIを起動）

BOSSはGUNSHIに以下を問いかけ、戦略的観点からの優先タスクを取得する：

```
「現在のフェーズ（[月]）を踏まえて、今日・今週やるべき最優先タスクを3〜5個に絞って教えてほしい。
今後の戦略.md（business-strategy-2025-2026.md）の優先アクションと、
master-strategy.md のコンテンツ戦略を参照した上で、実行可能性が高いものから優先して提示してほしい。」
```

GUNSHIが確認すべき観点：
- 現フェーズの最優先タスク（月次ロードマップ照合）
- 未着手の残課題のうち、ボトルネックになっているもの
- X・note・メルマガ・その他各チャネルのバランス
- 商品リリース・販売状況（`master-strategy.md` を参照）

---

### Step 3: 提案の統合・提示（BOSSが実行）

BOSSがGUNSHIの回答を統合し、以下の形式で提示する：

```
## 今日（今週）やること

**現在フェーズ**: [X月〜Y月フェーズ] / [フェーズの主テーマ]

---

### 最優先（必ずやる）
1. [具体的なアクション]
   → [期待効果 / 理由]

### 高優先（できればやる）
2. [具体的なアクション]
   → [期待効果 / 理由]

### 余裕があれば
3. [具体的なアクション]
   → [期待効果 / 理由]

---

**GUNSHIからの戦略コメント**:
[官兵衛の率直な一言 / 見落としの指摘 / 戦略的観点からの補足]
```

---

### Step 4: 実行支援の提案（BOSSが実行）

提案後、以下を問いかける：

```
「どれから始めますか？ 手伝えることがあれば、そのまま一緒に作業します。
例）X投稿を書く / メルマガ本文を作る / 商品設計を言語化する」
```

ユーザーが選んだタスクは、即座に対応するチームメイト（X_POST_CREATOR、NOTE_CREATOR等）に振り分けるか、BOSSが直接サポートする。

---

## 重要な判断軸

- **現フェーズ優先**: ロードマップの時期にあったタスクを選ぶ（先取りしすぎない）
- **実行可能性**: 週数時間という制約を考慮し、現実的なタスクに絞る
- **ボトルネック優先**: 他のタスクを止めている未解決事項を最優先に
- **ROI順**: メルマガ（ROI 4.6倍）> X発信 > note > オフライン の優先順位を意識

---

## ユーザーコンテキスト（常に前提として持つ）

以下のファイルを参照して把握すること：
- `ai-agent-organization/shared/knowledge/` → 組織共通の戦略・商品情報
- `ai-agent-organization/organization/BOSS/knowledge/knowhow/business-strategy-2025-2026.md` → 収益目標・活動期間
- `ai-agent-organization/organization/BOSS/knowledge/knowhow/strategy-brief.md` → フォロワー数・リソース制約・事業概要
