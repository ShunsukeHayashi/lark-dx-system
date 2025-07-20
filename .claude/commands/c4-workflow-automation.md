# C4: ワークフロー実装

## 指示
あなたはLark Baseの専門家です。自動化ワークフローを構築してください。

## T1: アラートワークフロー
`alert_workflow.json`として出力：

```json
{
  "workflow_name": "在庫切れ予測アラート",
  "description": "在庫が閾値を下回った際に自動通知",
  "trigger": {
    "type": "scheduled",
    "time": "09:00",
    "frequency": "daily",
    "target_table": "商品マスタ"
  },
  "conditions": [
    {
      "field": "在庫予測",
      "operator": "<",
      "value": 7
    },
    {
      "logic": "AND",
      "field": "フラグフィールド",
      "operator": "!=",
      "value": "処理済"
    }
  ],
  "actions": [
    {
      "type": "field_update",
      "updates": [
        {"field": "アラートステータス", "value": "🚨要対応"},
        {"field": "更新日時", "value": "NOW()"}
      ]
    },
    {
      "type": "notification",
      "to": "@{{担当者フィールド}}",
      "message": "{{商品名}}の在庫が残り{{在庫予測}}日です"
    },
    {
      "type": "record_create",
      "table": "発注タスク",
      "values": {
        "task_name": "{{商品名}}の発注実行",
        "deadline": "TODAY() + 3"
      }
    }
  ]
}
```

## T2: 承認ワークフロー
`approval_workflow.json`として出力：

```json
{
  "workflow_name": "金額承認フロー",
  "description": "金額や重要度に応じた多段階承認",
  "trigger": {
    "type": "field_update",
    "monitor_field": "ステータス",
    "condition": "'承認申請'に変更された時"
  },
  "conditions": [
    {
      "field": "金額",
      "operator": ">=",
      "value": "{{承認必要金額}}"
    },
    {
      "logic": "OR",
      "field": "重要度",
      "operator": "=",
      "value": "高"
    }
  ],
  "actions": [
    {
      "type": "approval_request",
      "approver": "{{承認者フィールド}}",
      "deadline": "3営業日",
      "on_approval": [
        {"field": "ステータス", "value": "承認済"},
        {"field": "承認日", "value": "TODAY()"},
        {"field": "承認者履歴", "value": "CONCATENATE({{承認者履歴}}, '; ', {{承認者}})"}
      ],
      "on_rejection": [
        {"field": "ステータス", "value": "差戻し"}
      ]
    },
    {
      "type": "reminder",
      "day1": "未承認の場合、承認者に再通知",
      "day3": "未承認の場合、上位承認者にエスカレーション"
    }
  ]
}
```

## T3: プロセスワークフロー
`process_workflow.json`として出力：

```json
{
  "workflow_name": "実績入力時自動処理",
  "description": "データ入力時の関連情報自動更新",
  "trigger": {
    "type": "field_update",
    "monitor_field": "実績フィールド",
    "condition": "値が入力された時"
  },
  "actions": [
    {
      "type": "related_update",
      "target": "関連テーブル.関連フィールド",
      "formula": "{{現在値}} - {{入力値}}"
    },
    {
      "type": "status_update",
      "updates": [
        {"field": "処理ステータス", "value": "完了"},
        {"field": "完了日", "value": "TODAY()"}
      ]
    },
    {
      "type": "next_process",
      "create_record": "次工程テーブル",
      "initial_values": [
        {"field": "参照ID", "value": "{{現在のID}}"},
        {"field": "開始日", "value": "TODAY()"}
      ]
    }
  ]
}
```