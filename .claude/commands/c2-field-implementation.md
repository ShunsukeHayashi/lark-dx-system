# C2: フィールド設計・実装

## 指示
あなたはLark Baseの専門家です。各テーブルのフィールドを詳細設計・実装してください。

## T0: 主キー設計 (最優先)
`primary_key_design.json`として出力：

```json
{
  "master_tables": {
    "primary_key": {
      "field_name": "エンティティ名",
      "type": "text",
      "position": "leftmost",
      "constraints": ["required", "unique"],
      "example": "株式会社ABC"
    }
  },
  "transaction_tables": {
    "primary_key": {
      "field_name": "トランザクションID",
      "type": "formula",
      "formula": "CONCATENATE(TEXT(日付, 'YYYY-MM-DD'), '_', 関連エンティティ, '_', LEFT(説明, 20))",
      "position": "leftmost",
      "example": "2024-01-15_ABC商事_定期メンテナンス実施"
    }
  },
  "preview_settings": {
    "display_fields": 3,
    "priority": ["ID", "ステータス", "金額/数量"]
  }
}
```

## T1: マスターフィールド
`master_fields.json`として出力：

```json
{
  "fields": [
    {
      "name": "ID",
      "type": "text/auto_number",
      "format": "MST-YYYY-0000"
    },
    {
      "name": "名称",
      "type": "text"
    },
    {
      "name": "カテゴリ",
      "type": "single_select",
      "options": [
        {"value": "カテゴリ1", "color": "🟢緑(1,5)"},
        {"value": "カテゴリ2", "color": "🔵青(1,7)"},
        {"value": "カテゴリ3", "color": "🟡黄(1,3)"}
      ]
    },
    {
      "name": "ステータス",
      "type": "single_select",
      "options": [
        {"value": "有効", "color": "🟢緑(1,5)"},
        {"value": "無効", "color": "🤍グレー(1,11)"}
      ]
    },
    {
      "name": "単価",
      "type": "currency",
      "currency": "JPY"
    },
    {
      "name": "在庫数",
      "type": "number"
    },
    {
      "name": "登録日",
      "type": "date"
    },
    {
      "name": "更新日",
      "type": "date"
    },
    {
      "name": "担当者",
      "type": "user",
      "multiple": false
    },
    {
      "name": "備考",
      "type": "text",
      "multiline": true
    }
  ]
}
```

## T2: トランザクションフィールド
`transaction_fields.json`として出力：

```json
{
  "fields": [
    {
      "name": "処理番号",
      "type": "auto_number",
      "format": "TRN-YYYYMMDD-0001"
    },
    {
      "name": "ステータス",
      "type": "single_select",
      "options": [
        {"value": "新規", "color": "🔵青"},
        {"value": "処理中", "color": "🟡黄"},
        {"value": "完了", "color": "🟢緑"},
        {"value": "キャンセル", "color": "🤍グレー"},
        {"value": "エラー", "color": "❤️赤"}
      ]
    },
    {
      "name": "優先度",
      "type": "single_select",
      "options": [
        {"value": "緊急", "color": "❤️赤"},
        {"value": "高", "color": "🟡黄"},
        {"value": "中", "color": "🔵青"},
        {"value": "低", "color": "🤍グレー"}
      ]
    },
    {
      "name": "金額",
      "type": "currency"
    },
    {
      "name": "税額",
      "type": "currency"
    },
    {
      "name": "合計",
      "type": "currency"
    },
    {
      "name": "開始日",
      "type": "date"
    },
    {
      "name": "期限",
      "type": "date"
    },
    {
      "name": "完了日",
      "type": "date"
    },
    {
      "name": "緊急フラグ",
      "type": "checkbox"
    },
    {
      "name": "承認フラグ",
      "type": "checkbox"
    }
  ]
}
```

## T3: 数式フィールド
`formula_fields.json`として出力：

```json
{
  "formulas": [
    {
      "name": "残日数",
      "formula": "IF(ステータス != '完了', 期限 - TODAY(), '完了済')",
      "type": "number/text"
    },
    {
      "name": "在庫予測",
      "formula": "IF(在庫 / 日次平均 < 7, '🚨緊急発注', IF(在庫 / 日次平均 < 14, '⚠️要確認', '✅正常'))",
      "type": "text"
    },
    {
      "name": "達成率",
      "formula": "IF(目標 > 0, 実績 / 目標 * 100, 0)",
      "type": "percent"
    },
    {
      "name": "アラート判定",
      "formula": "IF(残日数 < 0, '遅延', IF(残日数 < 3, '期限間近', '正常'))",
      "type": "text"
    }
  ]
}
```