# MAX Subscription トークンセットアップガイド

## 🔐 重要：セキュリティに関する注意

**⚠️ 警告：トークンは機密情報です**

提供されたトークン（`sk-ant-oat01-...`）は、あなたのClaude MAXアカウントへのアクセス権を持つ重要な認証情報です。

### セキュリティベストプラクティス

1. **絶対に公開しない**
   - GitHubのコードにハードコーディングしない
   - 公開リポジトリにコミットしない
   - チャットやメールで共有しない

2. **安全な保管方法**
   - GitHub Secretsに保存（推奨）
   - 環境変数として設定
   - パスワードマネージャーで管理

3. **定期的な更新**
   - トークンは定期的に再生成することを推奨
   - 漏洩の疑いがある場合は即座に無効化

## 📋 セットアップ手順

### 1. GitHub Secretsへの登録

1. GitHubリポジトリの `Settings` タブを開く
2. `Secrets and variables` → `Actions` を選択
3. `New repository secret` をクリック
4. 以下を入力：
   - **Name**: `CLAUDE_CODE_OAUTH_TOKEN`
   - **Secret**: 提供されたトークン（`sk-ant-oat01-...`）
5. `Add secret` をクリック

### 2. ワークフローの使用

MAX Subscription対応ワークフロー（`lark-base-builder-max.yml`）を使用：

```bash
# GitHub Actionsタブから実行
1. Actions → Lark Base Builder with MAX Subscription
2. Run workflow
3. パラメータ設定：
   - use_max_subscription: true（デフォルト）
```

### 3. トークンの確認

正しく設定されているか確認：
- Secretsページで `CLAUDE_CODE_OAUTH_TOKEN` が表示される
- 値は `***` でマスクされている

## 🚀 使用開始

1. ワークフローを実行
2. MAX Subscriptionの制限内で使用可能
3. API料金は発生しない

## ⚡ トラブルシューティング

### 認証エラーの場合

1. トークンが正しくコピーされているか確認
2. 前後の空白が含まれていないか確認
3. Secretの名前が正確か確認（`CLAUDE_CODE_OAUTH_TOKEN`）

### トークンの再生成

```bash
# ターミナルで実行
claude setup-token
```

## 📝 注意事項

- このトークンは個人のMAX Subscriptionに紐づいています
- 複数人での共有は利用規約違反の可能性があります
- チーム利用の場合は、各メンバーが個別のトークンを生成してください