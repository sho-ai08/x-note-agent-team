---
name: setup-org
description: AIエージェント組織を自動構築するスキル。「組織を作って」「セットアップして」「初期化して」などの依頼時に使用。
user-invocable: true
---

# 組織初期化スキル

ユーザーが組織構築を依頼しました。以下のフローで実行してください。

## Phase 1: ヒアリング

AskUserQuestionツールを使用して、以下を確認：

1. **組織の目的** - 何をする組織か、どんな課題を解決するか
2. **専門領域** - どの分野を専門とするか
3. **ターゲット** - 誰に向けたアウトプットを作るか
4. **品質基準** - 成果物に求める品質、守るべきガイドライン

## Phase 2: 共有ナレッジ生成

ヒアリング結果を元に以下のファイルを生成：

- `ai-agent-organization/shared/knowledge/noteの心得.md` - note公式方針
- 各エージェントのknowledge/knowhow/strategy-brief.md - ターゲット・ポジショニング
- `ai-agent-organization/system/config.yaml` の project セクションを更新

## Phase 3: エージェント作成提案

ヒアリングで確認したタスクに基づき、必要なエージェントを提案。
ユーザー承認後、Task toolでGENESISエージェント(subagent_type=GENESIS)を起動してエージェント作成を依頼。

## Phase 4: 完了報告

組織構成を報告：
- コアエージェント（BOSS, GENESIS, ARCHITECT）
- 新規作成した実働部隊エージェント
- 設定完了ファイル一覧
- 次のアクション例

$ARGUMENTS
