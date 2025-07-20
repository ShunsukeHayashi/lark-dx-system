# Lark Base 統合管理システム構築手順書

## 📋 目次

1. [システム概要](#システム概要)
2. [事前準備](#事前準備)
3. [構築手順](#構築手順)
4. [成果物の活用方法](#成果物の活用方法)
5. [運用・保守](#運用保守)
6. [FAQ](#faq)

---

## システム概要

### 目的
GitHub ActionsとClaude AIを活用し、Lark Base上に業界・業務領域に特化した統合管理システムを自動構築します。

### 特徴
- **完全自動化**: 設計から実装まで全工程をAIが自動実行
- **カスタマイズ可能**: 業界・業務領域に応じた最適化
- **並列処理**: 4つのトラックで効率的に構築
- **品質保証**: テスト・検証プロセスを含む

### 成果物
- 要件定義書・設計書（YAML/JSON形式）
- Lark Base実装ガイド
- テスト結果レポート
- 運用手順書

---

## 事前準備

### 1. 必要なアカウント

#### 1.1 GitHub アカウント
- [ ] GitHubアカウントを作成（https://github.com）
- [ ] リポジトリの作成権限を確認

#### 1.2 Claude アカウント（いずれか1つ）

**オプション1: Claude MAX Subscription（推奨）**
- [ ] Claude.aiでMAXプラン（月額$20）に登録
- [ ] メリット：追加料金なし、使い放題

**オプション2: Anthropic API**
- [ ] Anthropic Console（https://console.anthropic.com）でアカウント作成
- [ ] APIクレジットを購入（従量課金）

#### 1.3 Lark アカウント
- [ ] Larkアカウントを作成
- [ ] Lark Base（多維表格）の利用権限を確認

### 2. 環境準備

#### 2.1 リポジトリのセットアップ

1. **GitHubでフォーク**
   ```
   https://github.com/[your-org]/lark-base-builder
   → Fork ボタンをクリック
   ```

2. **ローカルにクローン**
   ```bash
   git clone https://github.com/[your-username]/lark-base-builder.git
   cd lark-base-builder
   ```

#### 2.2 認証情報の設定

**MAX Subscription利用の場合：**

1. ターミナルで実行：
   ```bash
   claude setup-token
   ```

2. ブラウザで認証：
   - 認証画面で「承認する」をクリック
   - 表示されたコードをコピー
   - ターミナルに貼り付けてEnter

3. GitHub Secretsに登録：
   - Settings → Secrets and variables → Actions
   - New repository secret
   - Name: `CLAUDE_CODE_OAUTH_TOKEN`
   - Value: 生成されたトークン

**API利用の場合：**
- Name: `ANTHROPIC_API_KEY`
- Value: APIキー（sk-ant-api03-...）

---

## 構築手順

### ステップ1: パラメータの決定

構築前に以下を決定してください：

| パラメータ | 説明 | 例 |
|-----------|------|-----|
| 業界 | 対象となる業界 | 小売業、製造業、医療 |
| 業務領域 | 管理したい業務 | 在庫管理、顧客管理、プロジェクト管理 |
| 規模 | 想定利用者数 | 5-50名 |
| データ量 | 管理対象数 | 1,000-10,000件 |

### ステップ2: ワークフローの実行

1. **GitHubでActionsタブを開く**
   ![Actions Tab](images/actions-tab.png)

2. **ワークフローを選択**
   - MAX利用: `Lark Base Builder with MAX Subscription`
   - API利用: `Lark Base Builder with Claude Code Base Action`

3. **Run workflowをクリック**

4. **パラメータを入力**
   ```
   業界: [あなたの業界]
   業務領域: [あなたの業務領域]
   Claudeモデル: claude-3-haiku-20240307（推奨）
   MAX Subscriptionを使用: true（MAX利用時）
   ```

5. **Run workflowボタンをクリック**

### ステップ3: 実行状況の確認

1. **進捗モニタリング**
   - 各トラックの実行状況をリアルタイムで確認
   - 緑のチェック✓ = 成功
   - 赤の×= エラー（ログを確認）

2. **並列実行トラック**
   | トラック | 内容 | 所要時間 |
   |---------|------|----------|
   | DataFoundation | テーブル・フィールド設計 | 約5-10分 |
   | Automation | ワークフロー・ボタン | 約5-10分 |
   | Visualization | ビュー・ダッシュボード | 約5-10分 |
   | OperationalReady | 権限・テスト・移行 | 約5-10分 |

### ステップ4: 成果物のダウンロード

1. **ワークフロー完了後**
   - Summaryセクションまでスクロール
   - Artifactsセクションを確認

2. **成果物をダウンロード**
   ```
   design-artifacts-DataFoundation.zip
   design-artifacts-Automation.zip
   design-artifacts-Visualization.zip
   design-artifacts-OperationalReady.zip
   ```

---

## 成果物の活用方法

### 1. 設計書の確認

各ZIPファイルを解凍し、以下のファイルを確認：

#### DataFoundation（データ基盤）
```
requirement_spec.yaml      # 要件定義
table_design.yaml         # テーブル設計
primary_key_design.json   # 主キー設計
master_fields.json        # マスターフィールド
transaction_fields.json   # トランザクションフィールド
formula_fields.json       # 数式フィールド
```

#### Automation（自動化）
```
alert_workflow.json       # アラートワークフロー
approval_workflow.json    # 承認ワークフロー
process_workflow.json     # プロセスワークフロー
quick_create_button.json  # クイック作成ボタン
external_link_button.json # 外部連携ボタン
batch_process_button.json # 一括処理ボタン
```

### 2. Lark Baseへの実装

#### 2.1 Base（多維表格）の作成

1. Larkにログイン
2. 「多維表格」→「新規作成」
3. 名前を入力（例：`[業界][業務]統合管理システム`）

#### 2.2 テーブルの作成

`table_design.yaml`を参照して：

1. **マスターテーブル作成**
   ```yaml
   例: 商品マスタ
   - テーブル名: 商品マスタ
   - 説明: 商品・サービスの基本情報管理
   ```

2. **トランザクションテーブル作成**
   ```yaml
   例: 注文テーブル
   - テーブル名: 注文管理
   - 説明: 受注・依頼の記録
   ```

#### 2.3 フィールドの設定

各JSONファイルを参照して、フィールドを作成：

**例: master_fields.json**
```json
{
  "name": "商品名",
  "type": "text",
  "required": true
}
```

Lark Baseでの操作：
1. テーブルを開く
2. 「+」ボタンでフィールド追加
3. タイプを選択（テキスト）
4. 名前を入力（商品名）
5. 必須設定をON

#### 2.4 ワークフローの設定

`alert_workflow.json`を参照して：

1. 自動化 → 新規ワークフロー
2. トリガー設定（例：毎日9:00）
3. 条件設定（例：在庫 < 7）
4. アクション設定（例：通知送信）

### 3. 実装チェックリスト

- [ ] 全テーブルが作成されている
- [ ] 主キーフィールドが最左端に配置されている
- [ ] リレーションが正しく設定されている
- [ ] ワークフローが動作している
- [ ] ビューが役割別に作成されている
- [ ] ダッシュボードが表示されている
- [ ] 権限設定が完了している

---

## 運用・保守

### 日次運用

1. **ダッシュボード確認**（5分）
   - KPI指標の確認
   - アラート対応

2. **ワークフロー監視**（5分）
   - 実行ログ確認
   - エラー対応

### 週次メンテナンス

1. **データ品質チェック**（30分）
   - 重複データ確認
   - 不整合データ修正

2. **パフォーマンス確認**（15分）
   - 処理時間測定
   - 必要に応じて最適化

### 月次レビュー

1. **利用状況分析**（1時間）
   - ユーザー別利用統計
   - 機能別利用頻度

2. **改善提案**（30分）
   - ユーザーフィードバック収集
   - 機能追加・修正計画

---

## FAQ

### Q1: エラーが発生した場合は？

**A:** GitHub Actionsのログを確認してください：
1. Failed jobをクリック
2. エラーメッセージを確認
3. 多くの場合、パラメータの誤りや権限不足が原因

### Q2: 一部のトラックだけ再実行したい

**A:** 個別実行用のワークフローを作成できます：
```yaml
matrix:
  track:
    - name: 'DataFoundation'  # これのみ残す
```

### Q3: カスタマイズしたい項目がある

**A:** `.claude/commands/`内のMarkdownファイルを編集：
- プロンプトの調整
- 出力形式の変更
- フィールドの追加・削除

### Q4: 複数の環境（開発・本番）で使いたい

**A:** ブランチ戦略を活用：
- `develop`ブランチ: 開発環境
- `main`ブランチ: 本番環境

### Q5: セキュリティが心配

**A:** 以下の対策を実施：
- GitHub Secretsで認証情報を保護
- プライベートリポジトリを使用
- 定期的なトークン更新

---

## サポート

### 技術サポート

- **GitHub Issues**: バグ報告・機能要望
- **メール**: support@example.com
- **ドキュメント**: https://docs.example.com

### コミュニティ

- **Slack**: #lark-base-builder
- **定期勉強会**: 毎月第3金曜日

### アップデート情報

- **リリースノート**: GitHub Releases
- **ブログ**: https://blog.example.com

---

## 付録

### A. 用語集

| 用語 | 説明 |
|------|------|
| Lark Base | Larkの多維表格（データベース機能） |
| GitHub Actions | CI/CDワークフロー自動化ツール |
| Claude | Anthropic社のAIアシスタント |
| MAX Subscription | Claude.aiの月額サブスクリプション |

### B. トラブルシューティング詳細

詳細なトラブルシューティングガイドは以下を参照：
- [GitHub Actions エラー対処法](troubleshooting/github-actions.md)
- [Lark Base 設定ガイド](troubleshooting/lark-base.md)
- [認証エラー解決方法](troubleshooting/authentication.md)

### C. ベストプラクティス

1. **命名規則**
   - テーブル: `[種別]_[用途]`（例：MST_商品）
   - フィールド: 日本語で分かりやすく

2. **データ管理**
   - 定期バックアップ（週1回）
   - テスト環境での事前検証

3. **パフォーマンス**
   - 数式は必要最小限に
   - ビューは役割別に最適化

---

**最終更新日**: 2025年7月20日  
**バージョン**: 1.0.0