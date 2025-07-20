# C3: リレーション構築

## 指示
あなたはLark Baseの専門家です。テーブル間の双方向リンクを設定してください。

## T0: 可視性チェック (最優先)
`visibility_optimization.json`として出力：

```json
{
  "bidirectional_links": {
    "parent_side": {
      "display": "関連レコード数",
      "aggregation": "COUNT"
    },
    "child_side": {
      "display": "親レコードの主要情報",
      "fields": ["ID", "名称", "ステータス"]
    }
  },
  "lookup_fields": [
    {
      "source": "取引先",
      "lookups": ["最終取引日", "累計金額", "担当営業"]
    },
    {
      "source": "商品",
      "lookups": ["在庫数", "単価", "カテゴリ"]
    },
    {
      "source": "プロジェクト",
      "lookups": ["進捗率", "期限", "担当者"]
    }
  ],
  "link_preview": {
    "max_fields": 3,
    "field_order": ["主キー", "ステータス", "金額/数量"]
  }
}
```

## T1: 準備確認
`relation_preparation.yaml`として出力：

```yaml
preparation_checklist:
  - all_tables_created: true
  - primary_keys_defined: true
  - relation_order:
    - "子テーブル → 親テーブルの順で設定"
    - "多:多の関係は最後に設定"
```

## T2: リンク作成
`bidirectional_links.json`として出力：

```json
{
  "links": [
    {
      "name": "注文→商品マスタ",
      "type": "many_to_one",
      "from_table": "注文",
      "from_field": "商品名",
      "to_table": "商品マスタ",
      "to_field": "商品ID",
      "selection": "single"
    },
    {
      "name": "注文→取引先マスタ",
      "type": "many_to_one",
      "from_table": "注文",
      "from_field": "取引先名",
      "to_table": "取引先マスタ",
      "to_field": "取引先ID",
      "selection": "single"
    },
    {
      "name": "タスク→プロジェクト",
      "type": "many_to_many",
      "from_table": "タスク",
      "from_field": "関連プロジェクト",
      "to_table": "プロジェクト",
      "to_field": "プロジェクトID",
      "selection": "multiple"
    }
  ]
}
```

## T3: ルックアップ作成
`lookup_fields.json`として出力：

```json
{
  "lookups": [
    {
      "name": "商品単価",
      "type": "lookup",
      "source": "商品.単価",
      "table": "注文"
    },
    {
      "name": "取引先情報",
      "type": "lookup",
      "source": "取引先.連絡先",
      "table": "注文"
    },
    {
      "name": "関連集計",
      "type": "lookup_with_aggregation",
      "source": "関連レコード.金額",
      "aggregation": "SUM",
      "table": "プロジェクト"
    }
  ]
}
```