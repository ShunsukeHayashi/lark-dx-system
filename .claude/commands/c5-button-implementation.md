# C5: ボタン実装

## 指示
あなたはLark Baseの専門家です。アクションボタンを設定してください。

## T1: クイック作成ボタン
`quick_create_button.json`として出力：

```json
{
  "button_name": "🚀簡易作成",
  "icon": "🚀",
  "placement": "メインテーブルの各レコード",
  "display_condition": "ステータス = '対象ステータス'",
  "execution_permission": "編集者以上",
  "action_flow": [
    {
      "step": 1,
      "action": "get_current_record",
      "data": [
        {"var": "参照ID", "value": "RECORD_ID()"},
        {"var": "デフォルト値1", "value": "{{フィールド1}}"},
        {"var": "デフォルト値2", "value": "{{フィールド2}}"}
      ]
    },
    {
      "step": 2,
      "action": "create_new_record",
      "table": "作成先テーブル",
      "initial_values": [
        {"field": "参照フィールド", "value": "{{参照ID}}"},
        {"field": "フィールドA", "value": "{{デフォルト値1}}"},
        {"field": "ステータス", "value": "新規作成"}
      ]
    },
    {
      "step": 3,
      "action": "completion_notification",
      "message": "{{名称}}を作成しました",
      "link": "作成したレコードへ"
    }
  ]
}
```

## T2: 外部連携ボタン
`external_link_button.json`として出力：

```json
{
  "button_name": "📞外部連携",
  "icon": "📞",
  "function": "外部サービスとの連携",
  "actions": [
    {
      "step": 1,
      "action": "get_contact_info",
      "data": [
        {"var": "連絡先", "value": "LOOKUP({{取引先}}, {{連絡先フィールド}})"},
        {"var": "テンプレート", "value": "LOOKUP({{取引先}}, {{テンプレートフィールド}})"}
      ]
    },
    {
      "step": 2,
      "action": "launch_app",
      "url": "{{アプリスキーム}}://{{連絡先}}",
      "message": "SUBSTITUTE({{テンプレート}}, '{{変数}}', {{値}})"
    },
    {
      "step": 3,
      "action": "record_history",
      "field": "連絡履歴",
      "value": "CONCATENATE({{連絡履歴}}, '\\n', TODAY(), ': 連絡実行')"
    }
  ]
}
```

## T3: 一括処理ボタン
`batch_process_button.json`として出力：

```json
{
  "button_name": "📊一括処理",
  "icon": "📊",
  "function": "関連レコードの一括更新",
  "actions": [
    {
      "step": 1,
      "action": "identify_targets",
      "condition": "関連フィールド = RECORD_ID()",
      "additional": "AND ステータス = '対象ステータス'"
    },
    {
      "step": 2,
      "action": "bulk_update",
      "update_fields": [
        {"field": "ステータス", "value": "新ステータス"},
        {"field": "処理日", "value": "TODAY()"},
        {"field": "処理者", "value": "CURRENT_USER()"}
      ]
    },
    {
      "step": 3,
      "action": "update_summary",
      "summary": [
        {"field": "処理済み数", "value": "COUNT(更新レコード)"},
        {"field": "未処理数", "value": "{{総数}} - {{処理済み数}}"}
      ]
    }
  ]
}
```