# C6: ビュー作成

各種ビューを作成・設定します。業務要件に応じて最適なビュータイプを選択し、ユーザーの役割に応じた表示を構成します。

## タスク実行手順

### T1: グリッドビュー作成
業務別のグリッドビューを作成します：

1. **管理者用ビュー**
   - 全フィールド表示
   - フィルター: なし
   - ソート: 優先度降順, 期日昇順
   - 条件付き書式: 期限による色分け

2. **担当者用ビュー**
   - 表示: 必要フィールドのみ
   - フィルター: 担当者 = CURRENT_USER()
   - 条件付き書式: 期限による色分け
   - グループ化: ステータス別

3. **分析用ビュー**
   - グループ化: カテゴリ
   - 集計行表示
   - ピボットテーブル形式
   - エクスポート可能設定

### T2: カンバンビュー作成
プロセス管理用のカンバンビューを構築：

```yaml
kanban_configuration:
  grouping_field: "ステータス"
  card_display:
    title: "案件名"
    sub_info: 
      - "担当者"
      - "期限"
    tags: 
      - "優先度"
      - "カテゴリ"
  color_coding: "緊急度による自動色分け"
  wip_limit: "各列最大10件"
  drag_drop: "有効"
```

### T3: カレンダービュー作成
スケジュール管理用のカレンダービューを設定：

```yaml
calendar_configuration:
  date_field: "予定日"
  event_display:
    primary: "タイトル"
    secondary: "詳細情報"
  color_scheme: "種別による自動色分け"
  filters:
    - "有効フラグ = true"
    - "担当者 = CURRENT_USER()"
  views:
    - "月表示"
    - "週表示"
    - "日表示"
```

## 出力例

### grid_views.json
```json
{
  "views": [
    {
      "name": "管理者用全体ビュー",
      "type": "grid",
      "fields": "all",
      "filters": [],
      "sort": [
        {"field": "優先度", "order": "desc"},
        {"field": "期日", "order": "asc"}
      ],
      "conditional_formatting": [
        {
          "condition": "残日数 < 7",
          "format": "row_color",
          "color": "red"
        },
        {
          "condition": "達成率 > 100",
          "format": "cell_color",
          "color": "green"
        }
      ],
      "permissions": ["admin", "manager"]
    },
    {
      "name": "担当者用ビュー",
      "type": "grid",
      "fields": ["ID", "案件名", "ステータス", "期限", "進捗"],
      "filters": [
        {"field": "担当者", "operator": "=", "value": "CURRENT_USER()"}
      ],
      "sort": [
        {"field": "期限", "order": "asc"}
      ],
      "grouping": {
        "field": "ステータス",
        "collapsed": false
      },
      "permissions": ["all"]
    }
  ]
}
```

### kanban_views.json
```json
{
  "kanban_views": [
    {
      "name": "プロセス管理ボード",
      "grouping_field": "ステータス",
      "columns": [
        {"value": "新規", "color": "blue", "wip_limit": 10},
        {"value": "処理中", "color": "yellow", "wip_limit": 5},
        {"value": "レビュー", "color": "orange", "wip_limit": 3},
        {"value": "完了", "color": "green", "wip_limit": null}
      ],
      "card_configuration": {
        "title_field": "案件名",
        "subtitle_fields": ["担当者", "期限"],
        "tag_fields": ["優先度", "カテゴリ"],
        "color_by": "緊急度",
        "cover_image": "添付ファイル"
      },
      "features": {
        "drag_drop": true,
        "quick_actions": true,
        "card_preview": true
      }
    }
  ]
}
```

### calendar_views.json
```json
{
  "calendar_views": [
    {
      "name": "スケジュール管理",
      "date_field": "予定日",
      "end_date_field": "完了予定日",
      "event_display": {
        "title": "タスク名",
        "time": "開始時刻",
        "location": "場所",
        "attendees": "参加者"
      },
      "color_coding": {
        "field": "タスク種別",
        "mapping": {
          "会議": "#4285f4",
          "作業": "#34a853",
          "レビュー": "#fbbc04",
          "締切": "#ea4335"
        }
      },
      "default_view": "month",
      "available_views": ["month", "week", "day", "agenda"],
      "filters": [
        {"field": "有効フラグ", "value": true},
        {"field": "参加者", "contains": "CURRENT_USER()"}
      ]
    }
  ]
}
```

## 追加ビュータイプ

### ガントチャートビュー
```yaml
gantt_view:
  name: "プロジェクト工程表"
  start_date: "開始日"
  end_date: "完了予定日"
  progress: "達成率"
  dependencies: "前工程"
  milestones: "重要日程"
  critical_path: true
```

### ギャラリービュー
```yaml
gallery_view:
  name: "商品カタログ"
  image_field: "メイン画像"
  title: "商品名"
  subtitle: "価格"
  description: "商品説明"
  layout: "card"
  columns: 4
```

## ビュー設計のベストプラクティス

1. **役割別ビューの作成**
   - 各ユーザーの業務に必要な情報のみを表示
   - 不要なフィールドは非表示に
   - 適切なフィルターの事前設定

2. **パフォーマンスの最適化**
   - 表示フィールドの最小化
   - 適切なページネーション設定
   - 重い計算フィールドの表示制限

3. **モバイル対応**
   - モバイル用の簡易ビュー作成
   - 重要フィールドの優先表示
   - タッチ操作に適したレイアウト

4. **ビューの命名規則**
   - 用途が明確な名前付け
   - 部門名・役割名を含める
   - バージョン管理の考慮

実行後は各ビューの動作確認を行い、ユーザーフィードバックに基づいて調整してください。