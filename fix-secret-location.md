# GitHub Secrets 登録場所の修正

## 現在の状況
- ❌ **Environment secrets** に登録されている（間違い）
- ✅ **Repository secrets** に登録する必要がある（正解）

## 修正手順

### 1. 正しいページへ移動

1. **Settings** タブ
2. 左サイドバーの **Secrets and variables** → **Actions**
3. 以下の2つのタブが表示されます：
   - **Secrets** タブ ← ここをクリック！
   - **Variables** タブ

### 2. Repository secrets セクションを確認

**Secrets** タブをクリックすると、以下のセクションが表示されます：

```
Repository secrets
[New repository secret] ボタン

Environment secrets  
CLAUDE_CODE_OAUTH_TOKEN ← 現在ここに登録されている
```

### 3. Repository secrets に新規登録

1. **Repository secrets** セクションの **New repository secret** ボタンをクリック
2. 以下を入力：
   - **Name**: `CLAUDE_CODE_OAUTH_TOKEN`
   - **Secret**: `sk-ant-oat01-...`（あなたのトークン）
3. **Add secret** をクリック

### 4. Environment から削除（オプション）

Environment secrets から削除したい場合：
1. Environment の `CLAUDE_CODE_OAUTH_TOKEN` の右側の設定アイコンをクリック
2. **Remove** または **Delete** を選択

## 確認方法

正しく設定されると：

```
Repository secrets
CLAUDE_CODE_OAUTH_TOKEN    Updated now

Environment secrets
(空または CLAUDE_CODE_OAUTH_TOKEN がない)
```

## なぜ Repository secrets が必要？

- **Repository secrets**: リポジトリ全体で使用可能
- **Environment secrets**: 特定の環境でのみ使用可能

GitHub Actionsワークフローは Repository secrets を参照するように設定されています：
```yaml
claude_code_oauth_token: ${{ secrets.CLAUDE_CODE_OAUTH_TOKEN }}
```