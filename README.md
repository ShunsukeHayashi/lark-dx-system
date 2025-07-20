# Lark Base Builder with GitHub Actions

このプロジェクトは、GitHub ActionsとClaude Codeを使用してLark Base統合管理システムを自動構築するためのフレームワークです。

## 🎉 アップデート情報

**2025年7月版**: Claude Code GitHub ActionsがMAX Subscriptionに対応しました！
- 従量課金APIに加えて、Claude MAX（月額$20）でも利用可能
- 追加料金なしでGitHub Actionsを実行できます

## 概要

- **自動化**: Claude AIを活用した設計書の自動生成
- **並列処理**: Git worktreeとmatrix戦略による効率的な並列実行
- **モジュール化**: C1-C10のコマンドで段階的にシステムを構築
- **再利用可能**: 業界・業務領域をパラメータ化

## セットアップ

### 1. 認証設定

#### オプション1: MAX Subscription（推奨）

Claude MAX（月額$20）をお持ちの方は、追加料金なしで利用できます。

1. **トークンの生成**
   ```bash
   claude setup-token
   ```
   - ブラウザで認証画面が開きます
   - 「承認する」をクリック
   - 表示された認証コードをターミナルに貼り付け
   - トークン（`sk-ant-oat01-...`）が生成されます

2. **GitHubへの登録**
   - リポジトリの `Settings` → `Secrets and variables` → `Actions`
   - `New repository secret` をクリック
   - 名前: `CLAUDE_CODE_OAUTH_TOKEN`
   - 値: 生成されたトークン

#### オプション2: Anthropic API（従量課金）

1. [Anthropic Console](https://console.anthropic.com)でアカウントを作成
2. API Keysセクションで新しいキーを生成
3. GitHubに登録：
   - 名前: `ANTHROPIC_API_KEY`
   - 値: `sk-ant-api03-...`（取得したAPIキー）

### 2. ワークフローの選択

#### MAX Subscription版（推奨）
`Lark Base Builder with MAX Subscription` を使用

#### 従量課金版
`Lark Base Builder with Claude Code Base Action` を使用

### 3. ワークフローの実行

1. リポジトリの `Actions` タブに移動
2. 使用するワークフローを選択
3. `Run workflow` をクリック
4. 以下のパラメータを入力：
   - **対象の業界**: 例: 小売業、製造業、サービス業
   - **対象の業務領域**: 例: 在庫管理、顧客管理、プロジェクト管理
   - **Claudeモデル**: 使用するモデル（デフォルト: claude-3-haiku-20240307）
     - `claude-3-haiku-20240307`: 最速・開発向け
     - `claude-3-sonnet-20240229`: バランス型
     - `claude-3-opus-20240229`: 最高性能
   - **MAX Subscriptionを使用**（MAX版のみ）: true/false

## ワークフローの構成

### 並列トラック

ワークフローは4つの並列トラックで実行されます：

| トラック | コマンド | 説明 |
|---------|---------|------|
| DataFoundation | C1→C2→C3 | システム分析、フィールド設計、リレーション構築 |
| Automation | C4→C5 | ワークフロー、ボタン実装 |
| Visualization | C6→C7 | ビュー作成、ダッシュボード構築 |
| OperationalReady | C8→C9→C10 | 権限設定、テスト、デプロイ |

### コマンド詳細

#### データ基盤トラック
- **C1**: システム構造分析・設計
  - 要件定義 (`requirement_spec.yaml`)
  - データ構造設計 (`table_design.yaml`)

- **C2**: フィールド設計・実装
  - 主キー設計 (`primary_key_design.json`)
  - マスターフィールド (`master_fields.json`)
  - トランザクションフィールド (`transaction_fields.json`)
  - 数式フィールド (`formula_fields.json`)

- **C3**: リレーション構築
  - 可視性最適化 (`visibility_optimization.json`)
  - 双方向リンク (`bidirectional_links.json`)
  - ルックアップフィールド (`lookup_fields.json`)

#### 自動化トラック
- **C4**: ワークフロー実装
  - アラートワークフロー (`alert_workflow.json`)
  - 承認ワークフロー (`approval_workflow.json`)
  - プロセスワークフロー (`process_workflow.json`)

- **C5**: ボタン実装
  - クイック作成ボタン (`quick_create_button.json`)
  - 外部連携ボタン (`external_link_button.json`)
  - 一括処理ボタン (`batch_process_button.json`)

#### 可視化トラック
- **C6**: ビュー作成
  - グリッドビュー (`grid_views.json`)
  - カンバンビュー (`kanban_views.json`)
  - カレンダービュー (`calendar_views.json`)

- **C7**: ダッシュボード構築
  - KPIカード (`kpi_cards.json`)
  - メイングラフ (`main_charts.json`)
  - アクションテーブル (`action_tables.json`)

#### 運用準備トラック
- **C8**: 権限設定
  - ロール定義 (`role_definition.yaml`)
  - テーブル権限 (`table_permissions.json`)
  - フィールド権限 (`field_permissions.json`)

- **C9**: テスト・検証
  - 単体テスト結果 (`unit_test_results.yaml`)
  - 統合テスト結果 (`integration_test_results.yaml`)
  - パフォーマンステスト結果 (`performance_test_results.yaml`)

- **C10**: デプロイ・移行
  - 移行ログ (`migration_log.yaml`)
  - ユーザー設定完了 (`user_setup_complete.yaml`)
  - 本番稼働チェックリスト (`go_live_checklist.yaml`)

## カスタムコマンドの使用

プロジェクトには再利用可能なカスタムコマンドが含まれています：

```bash
# システム分析を実行
/c1-system-analysis [業界] [業務領域]

# フィールド設計を実行
/c2-field-implementation

# リレーション構築を実行
/c3-relation-setup

# 他のコマンドも同様に使用可能
```

## 成果物

ワークフローの実行により、以下が生成されます：

1. **設計書**: 各コマンドに対応するJSON/YAMLファイル
2. **ブランチ**: 各トラック用のフィーチャーブランチ
3. **アーティファクト**: Actions画面からダウンロード可能な成果物

## ローカル開発

### Git Worktreeを使用した並列開発

```bash
# 新しいworktreeを作成
git worktree add ../Lark-feature -b feature/local-development

# worktreeに移動
cd ../Lark-feature

# Claude Codeを実行
claude

# カスタムコマンドを使用
/c1-system-analysis 小売業 在庫管理
```

### worktreeの管理

```bash
# worktree一覧を表示
git worktree list

# 不要になったworktreeを削除
git worktree remove ../Lark-feature
```

## 料金について

### 料金体系

| プラン | 月額料金 | API料金 | 用途 |
|--------|----------|---------|------|
| MAX Subscription | $20/月 | なし | 個人開発・小規模チーム |
| Anthropic API | なし | 従量課金 | 大規模・商用利用 |

### API料金（従量課金の場合）

| モデル | 入力 (1Mトークン) | 出力 (1Mトークン) | 用途 |
|--------|-------------------|-------------------|------|
| Claude 3 Haiku | $0.25 | $1.25 | 開発・テスト |
| Claude 3 Sonnet | $3.00 | $15.00 | 本番環境 |
| Claude 3 Opus | $15.00 | $75.00 | 高精度が必要な場合 |

### コスト最適化のヒント

1. **MAX Subscriptionの活用**（月額固定で使い放題）
2. **開発時はHaikuを使用**
3. **必要なトラックのみ実行**

## トラブルシューティング

### APIキーエラー
- `ANTHROPIC_API_KEY`シークレットが正しく設定されているか確認
- APIキーの有効性を確認

### ワークフロー失敗
- Actionsログで詳細なエラーメッセージを確認
- 各ジョブのステップごとの出力を確認

### 依存関係エラー
- Claude CLIのインストールステップが成功しているか確認
- ネットワーク接続を確認

## 貢献

プロジェクトへの貢献を歓迎します：

1. Issueで改善提案や問題報告
2. Pull Requestで機能追加や修正
3. ドキュメントの改善

## ライセンス

このプロジェクトはMITライセンスの下で公開されています。