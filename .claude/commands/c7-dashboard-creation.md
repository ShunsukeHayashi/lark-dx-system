# C7: ダッシュボード構築

分析ダッシュボードを構築し、KPIの可視化と意思決定支援を実現します。

## 標準ダッシュボードレイアウト

```
┌─────────────────────────────────────────────────────────┐
│                    KPIカード層                          │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐  │
│  │ KPI1     │ │ KPI2     │ │ KPI3     │ │ KPI4     │  │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘  │
├─────────────────────────────────────────────────────────┤
│                    グラフ層                             │
│  ┌────────────────────┐     ┌────────────────────┐    │
│  │   メイングラフ     │     │   サブグラフ       │    │
│  └────────────────────┘     └────────────────────┘    │
├─────────────────────────────────────────────────────────┤
│                    詳細テーブル層                       │
│  ┌─────────────────────────────────────────────────┐    │
│  │            アクションテーブル                   │    │
│  └─────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────┘
```

## タスク実行手順

### T1: KPIカード作成

上部に配置する4つの主要KPIカードを作成：

```yaml
kpi_cards:
  - card1:
      name: "🚨緊急対応件数"
      formula: "COUNTIF(ステータス, '緊急')"
      display_type: "number"
      color_rules:
        - condition: "value = 0"
          color: "green"
        - condition: "value BETWEEN 1 AND 5"
          color: "yellow"
        - condition: "value > 5"
          color: "red"
      click_action: "filter_view"
      refresh_interval: "5min"

  - card2:
      name: "💰本日売上"
      formula: "SUMIF(日付, TODAY(), 金額)"
      display_type: "currency"
      comparison: "前日比"
      trend_indicator: true
      format: "¥#,##0"

  - card3:
      name: "📈達成率"
      formula: "(実績 / 目標) * 100"
      display_type: "percentage"
      visualization: "gauge"
      target_line: 100
      color_zones:
        - range: [0, 80]
          color: "red"
        - range: [80, 100]
          color: "yellow"
        - range: [100, 120]
          color: "green"

  - card4:
      name: "⏱️平均処理時間"
      formula: "AVG(完了日 - 開始日)"
      display_type: "duration"
      unit: "days"
      trend_arrow: true
      benchmark: 3
```

### T2: メイングラフ作成

ダッシュボードの中央に配置するグラフを構築：

```json
{
  "main_charts": [
    {
      "name": "月別売上推移",
      "type": "line_chart",
      "data_source": "売上テーブル",
      "x_axis": {
        "field": "月",
        "type": "date",
        "format": "YYYY-MM"
      },
      "y_axis": [
        {
          "field": "売上",
          "type": "currency",
          "color": "#4285f4"
        },
        {
          "field": "利益",
          "type": "currency",
          "color": "#34a853",
          "axis": "secondary"
        }
      ],
      "features": {
        "data_labels": true,
        "trend_line": true,
        "forecast": 3,
        "zoom": true
      }
    },
    {
      "name": "カテゴリ別売上",
      "type": "bar_chart",
      "orientation": "vertical",
      "data_source": "売上集計ビュー",
      "category": "カテゴリ",
      "value": "売上額",
      "sort": "descending",
      "limit": 10,
      "features": {
        "value_labels": true,
        "percentage": true
      }
    }
  ]
}
```

### T3: アクションテーブル作成

即座の対応が必要な項目を表示するテーブル：

```json
{
  "action_table": {
    "name": "要対応リスト",
    "data_source": "タスクテーブル",
    "filters": [
      {
        "field": "ステータス",
        "operator": "IN",
        "values": ["緊急", "要確認", "遅延"]
      }
    ],
    "columns": [
      {
        "field": "案件名",
        "width": "30%",
        "clickable": true
      },
      {
        "field": "期限",
        "width": "15%",
        "format": "date",
        "conditional_format": {
          "overdue": "red",
          "today": "orange",
          "upcoming": "yellow"
        }
      },
      {
        "field": "担当者",
        "width": "15%",
        "display": "user_avatar"
      },
      {
        "field": "優先度",
        "width": "10%",
        "display": "badge"
      },
      {
        "field": "アクション",
        "width": "30%",
        "type": "button_group",
        "buttons": [
          "詳細確認",
          "ステータス更新",
          "担当者変更"
        ]
      }
    ],
    "sort": [
      {"field": "優先度", "order": "desc"},
      {"field": "期限", "order": "asc"}
    ],
    "pagination": {
      "enabled": true,
      "page_size": 20
    }
  }
}
```

## 出力例

### kpi_cards.json
```json
{
  "kpi_configuration": {
    "layout": "horizontal",
    "cards": [
      {
        "id": "urgent_count",
        "position": 1,
        "title": "🚨緊急対応件数",
        "data_source": {
          "table": "タスクテーブル",
          "formula": "COUNTIF(ステータス, '緊急')"
        },
        "display": {
          "type": "big_number",
          "format": "integer",
          "size": "large"
        },
        "styling": {
          "background": "dynamic",
          "rules": [
            {"min": 0, "max": 0, "color": "#34a853"},
            {"min": 1, "max": 5, "color": "#fbbc04"},
            {"min": 6, "max": null, "color": "#ea4335"}
          ]
        },
        "interaction": {
          "clickable": true,
          "action": "filter_table",
          "target": "タスクテーブル",
          "filter": "ステータス = '緊急'"
        }
      }
    ]
  }
}
```

### main_charts.json
```json
{
  "chart_configuration": [
    {
      "id": "monthly_trend",
      "type": "combo_chart",
      "title": "月別売上・利益推移",
      "position": {
        "row": 2,
        "column": "left",
        "width": "60%"
      },
      "data": {
        "primary_axis": {
          "field": "月",
          "type": "datetime",
          "interval": "month"
        },
        "series": [
          {
            "name": "売上",
            "field": "売上額",
            "type": "column",
            "color": "#4285f4",
            "axis": "left"
          },
          {
            "name": "利益",
            "field": "利益額",
            "type": "line",
            "color": "#34a853",
            "axis": "left"
          },
          {
            "name": "利益率",
            "field": "利益率",
            "type": "line",
            "color": "#ea4335",
            "axis": "right",
            "format": "percentage"
          }
        ]
      },
      "options": {
        "legend": "top",
        "grid": true,
        "tooltip": true,
        "animation": true
      }
    }
  ]
}
```

### action_tables.json
```json
{
  "action_table_configuration": {
    "id": "urgent_tasks",
    "title": "要対応タスク一覧",
    "position": {
      "row": 3,
      "column": "full",
      "height": "auto"
    },
    "data_source": {
      "table": "タスクテーブル",
      "view": "緊急対応ビュー"
    },
    "display_options": {
      "row_height": "compact",
      "alternating_rows": true,
      "hover_highlight": true,
      "sticky_header": true
    },
    "interactive_features": {
      "inline_edit": ["ステータス", "担当者"],
      "bulk_actions": true,
      "export": ["csv", "excel"],
      "real_time_update": true
    }
  }
}
```

## ダッシュボードタイプ別テンプレート

### 1. 経営ダッシュボード
```yaml
executive_dashboard:
  kpis:
    - 月次売上
    - 前年同月比
    - 営業利益率
    - 顧客満足度
  charts:
    - 売上トレンド（過去12ヶ月）
    - 部門別業績
    - 地域別売上構成
  tables:
    - 重要プロジェクト進捗
    - 主要KPI達成状況
```

### 2. 業務ダッシュボード
```yaml
operational_dashboard:
  kpis:
    - 本日の処理件数
    - 平均処理時間
    - エラー率
    - SLA達成率
  charts:
    - 時間帯別処理量
    - プロセス別所要時間
    - エラー発生傾向
  tables:
    - 処理待ちキュー
    - エラー一覧
```

### 3. 分析ダッシュボード
```yaml
analytics_dashboard:
  kpis:
    - データ品質スコア
    - 異常検知数
    - 予測精度
    - トレンド変化率
  charts:
    - 相関分析
    - 時系列予測
    - 分布図
  tables:
    - 異常値詳細
    - 予測vs実績
```

## 実装時の注意点

1. **パフォーマンス最適化**
   - 重い集計は事前計算
   - 適切なキャッシュ設定
   - 段階的なデータ読み込み

2. **レスポンシブデザイン**
   - モバイル対応レイアウト
   - タブレット最適化
   - 自動サイズ調整

3. **リアルタイム性**
   - 更新頻度の適切な設定
   - WebSocket活用
   - 差分更新の実装

4. **アクセス制御**
   - 役割別ダッシュボード
   - 機密情報のマスキング
   - 監査ログの記録

実装完了後は、ユーザーの利用状況を分析し、継続的な改善を行ってください。