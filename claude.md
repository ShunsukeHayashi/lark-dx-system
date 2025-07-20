# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a Lark Base system design and implementation project using a documentation-driven approach. The project focuses on building a comprehensive DX (Digital Transformation) management system for Lark DX company using the Lark Base platform.

## Project Structure

```
.claude/Instructions/
├── workflow.md     # Log-Driven Development (LDD) methodology
├── metrics.md      # Metrics collection and analysis system
├── logging.md      # Structured logging framework
└── feedback.md     # Continuous improvement system

claude.md           # Main Lark Base framework instructions (105KB)
lark-dx-system-design.md  # Current system implementation specs
```

## Development Methodology

This project follows **Log-Driven Development (LDD)** approach:
- All activities must be logged and tracked
- Metrics-focused decision making
- Continuous feedback loops
- Structured logging in categories: tasks, system, feedback, metrics

## Command Stack Implementation (C1-C10)

The system is built using a sequential command stack:

1. **C1: システム構造分析・設計** - System analysis and design
2. **C2: フィールド設計・実装** - Field design and implementation
3. **C3: リレーション構築** - Relationship building
4. **C4: ワークフロー実装** - Workflow implementation
5. **C5: ボタン実装** - Button implementation
6. **C6: ビュー作成** - View creation
7. **C7: ダッシュボード構築** - Dashboard construction
8. **C8: 権限設定** - Permission settings
9. **C9: テスト・検証** - Testing and validation
10. **C10: デプロイ・移行** - Deployment and migration

Execute with: `C[number] run` or `ALL RUN` for complete implementation.

## Lark Base Specific Guidelines

### Field Types
- Primary keys must be positioned at the leftmost column
- Master tables use direct input primary keys
- Transaction tables use formula-based composite keys
- Date format in keys: YYYY-MM-DD
- Separator in composite keys: underscore (_)

### Color Coding Standards
- Emergency/Danger: ❤️ Red (row 1, position 1)
- Warning/Caution: 🟡 Yellow (row 1, position 3)
- Normal/Complete: 💚 Green (row 1, position 5)
- Info/Processing: 🔵 Blue (row 1, position 7)
- Inactive/Pending: 🤍 Gray (row 1, position 11)

### Workflow Patterns
- Alert workflows: Daily scheduled at 09:00
- Approval workflows: 3 business days deadline
- Process automation: Status-based triggers

## Current Implementation Status

The project is implementing a DX consulting management system with:
- Customer management (顧客マスタ)
- Project tracking (案件管理)
- Task management (プロジェクトタスク)
- Effect measurement (効果測定)

Target: 10-50 users, 100+ companies, 200-500 monthly transactions

## Important Notes

- This is NOT a traditional code repository - it's a Lark Base system design project
- No package.json, build scripts, or test commands exist
- All implementation is done through Lark Base platform configuration
- Documentation in Japanese is intentional and should be preserved
- The main instructions file (claude.md) contains comprehensive Lark Base framework details

## Key References

- Main framework: `/claude.md` - Complete Lark Base implementation framework
- Current design: `/lark-dx-system-design.md` - Specific implementation for Lark DX
- LDD methodology: `.claude/Instructions/workflow.md`

## Original Instructions

The following are the original instructions that should be followed:
 - # 全体目標設定
    - project_goal:
        - goal: "{{業界}}{{業務領域}}向けのLark
Base統合管理システムを構築する"
        - output: "完全に動作するLark Baseアプリケーション（テーブル、ビュー、ワークフロー、ダッシュボード含む）"
        - reference: "Lark Base公式ドキュメント、ベストプラクティス集"
 - コンテキスト
    - # メタ情報
        - meta:
            - title: "Lark Base汎用システム構築フレームワーク
- 完全統合版"
            - version: "2.0"
            - description: "業界・業務に依存しない汎用的なLark
Baseシステム構築のための完全なコマンドスタック"
            - last_updated: "2024-01-20"
    - # 実装フェーズテンプレート
        - implementation_phases:
            - phase0_preparation:
                - duration: "3日間"
                - day1_environment:
                    - - "Lark Baseワークスペース作成"
                    - - "管理者アカウント設定"
                    - - "チームメンバー招待"
                    - - "基本設定（タイムゾーン、言語）"
                - day2_data:
                    - - "既存データのエクスポート"
                    - - "データクレンジング"
                    - - "マスターデータ整理"
                    - - "インポート用CSV作成"
                - day3_design:
                    - - "テーブル設計書レビュー"
                    - - "ワークフロー設計確認"
                    - - "権限設計の承認"
                    - - "実装スケジュール確定"
            - phase1_foundation:
                - duration: "2週間"
                - week1_tables:
                    - day1_2_master:
                        - - "主キー設定"
                        - - "基本フィールド作成"
                        - - "選択肢設定"
                        - - "数式フィールド作成"
                    - day3_4_transaction:
                        - - "自動採番設定"
                        - - "ステータス管理"
                        - - "日付管理"
                        - - "金額計算"
                    - day5_7_data:
                        - - "マスターデータ投入"
                        - - "テストデータ作成"
                        - - "動作確認"
                - week2_relations:
                    - day8_9_links:
                        - - "1:N関係構築"
                        - - "N:N関係構築"
                        - - "参照整合性確認"
                    - day10_11_lookups:
                        - - "参照フィールド作成"
                        - - "集計フィールド設定"
                        - - "表示最適化"
                    - day12_14_testing:
                        - - "全リレーション確認"
                        - - "データ整合性チェック"
                        - - "パフォーマンステスト"
            - phase2_automation:
                - duration: "1週間"
                - day15_16_alerts:
                    - - "閾値監視ワークフロー"
                    - - "期限アラート"
                    - - "異常検知通知"
                - day17_18_process:
                    - - "承認フロー構築"
                    - - "ステータス自動更新"
                    - - "連携処理"
                - day19_21_buttons:
                    - - "ワンクリックボタン"
                    - - "一括処理ボタン"
                    - - "外部連携ボタン"
                    - - "動作テスト"
            - phase3_optimization:
                - duration: "1週間"
                - day22_23_views:
                    - - "役割別ビュー作成"
                    - - "分析ビュー構築"
                    - - "モバイルビュー最適化"
                - day24_25_dashboards:
                    - - "KPIダッシュボード"
                    - - "管理ダッシュボード"
                    - - "分析ダッシュボード"
                - day26_28_finalization:
                    - - "権限設定実装"
                    - - "通知設定最適化"
                    - - "ユーザー受入テスト"
                    - - "マニュアル作成"
    - # Lark Base フィールドタイプ完全ガイド
        - field_types_guide:
            - basic_field_types:
                - text:
                    - usage: "識別子、名称、コード"
                    - settings: "最大長、必須、ユニーク"
                    - examples: "{{識別コード}}、{{商品名}}"
                - number:
                    - usage: "数量、カウント、率"
                    - settings: "最小値、最大値、小数点桁数"
                    - examples: "{{在庫数}}、{{販売数}}"
                - currency:
                    - usage: "金額表示"
                    - settings: "通貨種類（JPY/USD/CNY等）、小数点"
                    - examples: "{{単価}}、{{原価}}"
                - date_datetime:
                    - usage: "期日管理、履歴記録"
                    - settings: "日付のみ/日時、デフォルト値"
                    - examples: "{{発注日}}、{{到着予定日}}"
                - single_select:
                    - usage: "ステータス、カテゴリ"
                    - settings: "選択肢と色の組み合わせ"
                    - examples: "{{ステータス}}、{{カテゴリ}}"
                - multi_select:
                    - usage: "タグ、複数属性"
                    - settings: "選択肢リスト"
                    - examples: "{{適用商品}}、{{対応チャネル}}"
                - checkbox:
                    - usage: "フラグ、真偽値"
                    - settings: "デフォルト値（true/false）"
                    - examples: "{{緊急フラグ}}、{{有効フラグ}}"
                - user:
                    - usage: "担当者、承認者"
                    - settings: "単一/複数選択"
                    - examples: "{{担当者}}、{{承認者}}"
                - attachment:
                    - usage: "画像、文書"
                    - settings: "最大ファイル数、対応形式"
                    - examples: "{{商品画像}}、{{契約書}}"
                - formula:
                    - usage: "自動計算"
                    - settings: "計算式"
                    - examples: "{{利益率}}、{{在庫予測}}"
    - # Lark Base 色指定ルール
        - color_palette_rules:
            - title: "Lark Base標準色パレット位置"
            - structure:
                - row1: "❤️赤 | 🧡オレンジ | 🟡黄 |
🟨淡黄 | 💚緑 | 🟩淡緑 | 🔵青 | 🔷淡青
| 💜紫 | 🟪淡紫 | 🤍グレー"
                - row2: "各色の淡色バージョン"
                - row3: "各色の濃色バージョン"
                - row4: "各色の最濃色バージョン"
            - usage_examples:
                - emergency_danger: "❤️標準赤（1行目1番目）"
                - warning_caution: "🟡標準黄（1行目3番目）"
                - normal_complete: "💚標準緑（1行目5番目）"
                - info_processing: "🔵標準青（1行目7番目）"
                - inactive_pending: "🤍標準グレー（1行目11番目）"
    - # ワークフロー設定の標準パターン
        - workflow_patterns:
            - trigger_types:
                - - "レコード作成時"
                - - "レコード更新時"
                - - "フィールド更新時"
                - - "定期実行（時刻指定）"
                - - "手動実行"
            - action_types:
                - - "フィールド値の更新"
                - - "通知送信（メンション）"
                - - "レコード作成"
                - - "外部連携（API）"
                - - "承認リクエスト"
            - standard_workflows:
                - alert_workflow:
                    - name: "{{指標}}切れ予測アラート"
                    - description: "{{指標}}が閾値を下回った際に自動通知"
                    - trigger:
                        - type: "定期実行"
                        - time: "毎日 09:00"
                        - target_table: "{{マスタテーブル}}"
                    - conditions:
                        - - "{{予測フィールド}} < {{閾値}}"
                        - - "AND {{フラグフィールド}}
!= '処理済'"
                    - actions:
                        - field_update:
                            - - "{{アラートフィールド}} = '
🚨要対応'"
                            - - "{{更新日時}} = NOW()"
                        - notification:
                            - to: "@{{担当者フィールド}}"
                            - message: "{{名称フィールド}}の{{指標}}が残り{{予測フィールド}}日です"
                        - record_create:
                            - table: "{{タスクテーブル}}"
                            - task_name: "{{名称フィールド}}の{{アクション}}実行"
                            - deadline: "TODAY() + 3"
                - approval_workflow:
                    - name: "{{プロセス}}承認フロー"
                    - description: "金額や重要度に応じた多段階承認"
                    - trigger:
                        - type: "フィールド更新"
                        - monitor_field: "{{ステータス}}"
                        - condition: "'承認申請' に変更された時"
                    - conditions:
                        - - "{{金額フィールド}} >= {{承認必要金額}}"
                        - - "OR {{重要度フィールド}} =
'高'"
                    - actions:
                        - approval_request:
                            - approver: "{{承認者フィールド}}"
                            - deadline: "3営業日"
                            - on_approval:
                                - - "{{ステータス}} = '承認済'"
                                - - "{{承認日}} = TODAY()"
                                - - "{{承認者履歴}} =
CONCATENATE({{承認者履歴}}, ';
', {{承認者}})"
                        - reminder:
                            - day1: "未承認の場合、承認者に再通知"
                            - day3: "未承認の場合、上位承認者にエスカレーション"
                - auto_process_workflow:
                    - name: "{{入力}}時自動処理"
                    - description: "データ入力時の関連情報自動更新"
                    - trigger:
                        - type: "フィールド更新"
                        - monitor_field: "{{実績フィールド}}"
                        - condition: "値が入力された時"
                    - actions:
                        - related_update:
                            - target: "{{関連テーブル}}.{{関連フィールド}}"
                            - formula: "{{現在値}} + {{入力値}}"
                        - status_update:
                            - - "{{プロセスステータス}} =
'完了'"
                            - - "{{完了日}} = TODAY()"
                        - next_process:
                            - create_record: "{{次工程テーブル}}"
                            - initial_values:
                                - - "{{参照ID}} = {{現在のID}}"
                                - - "{{開始日}} = TODAY()"
    - # ビュータイプと使用場面
        - view_types_usage:
            - grid_view:
                - usage: "データ一覧、詳細確認、一括編集"
                - settings:
                    - - "表示フィールド選択"
                    - - "フィルター条件"
                    - - "ソート順"
                    - - "条件付き書式"
                    - - "グループ化"
                - example:
                    - name: "{{管理対象}}一覧"
                    - filter: "{{ステータス}} != '無効'"
                    - sort: "{{優先度}} 降順, {{期日}}
昇順"
                    - conditional_format:
                        - - "{{残日数}} < 7: 行全体を赤色"
                        - - "{{達成率}} > 100%: セルを緑色"
            - kanban_view:
                - usage: "プロセス管理、ステータス管理、ドラッグ&ドロップ操作"
                - settings:
                    - - "グループ化フィールド（列）"
                    - - "カード表示フィールド"
                    - - "カード色分け"
                    - - "WIP制限"
                - example:
                    - name: "{{プロセス}}管理ボード"
                    - grouping: "{{ステータス}}"
                    - card_content:
                        - title: "{{案件名}}"
                        - sub_info: "{{担当者}}, {{期限}}"
                        - tags: "{{優先度}}, {{カテゴリ}}"
                    - color_coding: "{{緊急度}}による自動色分け"
            - calendar_view:
                - usage: "スケジュール管理、期日管理"
                - settings:
                    - - "日付フィールド"
                    - - "表示期間"
                    - - "イベント表示内容"
                    - - "色分け"
                - example:
                    - name: "{{納期}}カレンダー"
                    - date_field: "{{予定日}}"
                    - event_display:
                        - - "{{案件名}}"
                        - - "{{数量}}"
                        - - "{{担当者}}"
                    - color_coding: "{{プロセス種別}}"
            - gantt_chart:
                - usage: "プロジェクト管理、工程管理"
                - settings:
                    - - "開始日フィールド"
                    - - "終了日フィールド"
                    - - "進捗率フィールド"
                    - - "依存関係"
                - example:
                    - name: "{{プロジェクト}}工程表"
                    - duration: "{{開始日}} 〜 {{完了予定日}}"
                    - progress: "{{達成率}}"
                    - milestone: "{{重要日程}}"
            - gallery_view:
                - usage: "画像中心の表示、カタログ表示"
                - settings:
                    - - "画像フィールド"
                    - - "タイトルフィールド"
                    - - "説明フィールド"
                    - - "レイアウト"
                - example:
                    - name: "{{商品}}カタログ"
                    - image: "{{メイン画像}}"
                    - display_info:
                        - - "{{商品名}}"
                        - - "{{価格}}"
                        - - "{{在庫状況}}"
    - # ボタンフィールドの実装パターン
        - button_implementation_patterns:
            - basic_structure:
                - button_name: "{{アクション名}}"
                - icon: "{{絵文字}}（🚀 📞 📧 📊 💰
等）"
                - placement: "{{テーブル名}}の各レコード"
                - display_condition: "{{条件フィールド}}
= {{値}}"
                - execution_permission: "{{権限レベル}}"
                - action_flow:
                    - - "データ取得"
                    - - "処理実行"
                    - - "結果更新"
                    - - "通知送信"
            - standard_patterns:
                - one_click_creation:
                    - button_name: "🚀{{簡易作成}}"
                    - function: "関連レコードの即座作成"
                    - actions:
                        - get_current_record:
                            - - "{{参照ID}} = RECORD_ID()"
                            - - "{{デフォルト値1}} = {{フィールド1}}"
                            - - "{{デフォルト値2}} = {{フィールド2}}"
                        - create_new_record:
                            - table: "{{作成先テーブル}}"
                            - initial_values:
                                - - "{{参照フィールド}} = {{参照ID}}"
                                - - "{{フィールドA}} = {{デフォルト値1}}"
                                - - "{{ステータス}} = '新規作成'"
                        - completion_notification:
                            - message: "{{名称}}を作成しました"
                            - link: "作成したレコードへ"
                - external_integration:
                    - button_name: "📞{{連絡}}"
                    - function: "外部サービスとの連携"
                    - actions:
                        - get_contact_info:
                            - - "{{連絡先}} = LOOKUP({{取引先}},
{{連絡先フィールド}})"
                            - - "{{テンプレート}} =
LOOKUP({{取引先}}, {{テンプレートフィールド}})"
                        - launch_app:
                            - url: "{{アプリスキーム}}://{{連絡先}}"
                            - message: "SUBSTITUTE({{テンプレート}},
'{{変数}}', {{値}})"
                        - record_history:
                            - field: "{{連絡履歴}}"
                            - value: "CONCATENATE({{連絡履歴}},
'\n', TODAY(), ': 連絡実行')"
                - batch_processing:
                    - button_name: "📊{{一括更新}}"
                    - function: "関連レコードの一括更新"
                    - actions:
                        - identify_targets:
                            - condition: "{{関連フィールド}}
= RECORD_ID()"
                            - additional: "AND {{ステータス}}
= '{{対象ステータス}}'"
                        - bulk_update:
                            - update_fields:
                                - - "{{ステータス}} = '{{新ステータス}}'"
                                - - "{{処理日}} = TODAY()"
                                - - "{{処理者}} =
CURRENT_USER()"
                        - update_summary:
                            - - "{{処理済み数}} =
COUNT(更新レコード)"
                            - - "{{未処理数}} = {{総数}} -
{{処理済み数}}"
    - # ダッシュボード構築の標準レイアウト
        - dashboard_layout:
            - basic_structure: |
                - ┌─────────────────────────────────────────────────────────┐
                - │                    KPIカード層
                          │
                - │  ┌──────────┐
┌──────────┐
┌──────────┐
┌──────────┐  │
                - │  │ {{KPI1}}  │ │ {{KPI2}}  │
│ {{KPI3}}  │ │ {{KPI4}}  │  │
                - │  └──────────┘
└──────────┘
└──────────┘
└──────────┘  │
                - ├─────────────────────────────────────────────────────────┤
                - │                    グラフ層
                            │
                - │
 ┌────────────────────┐
    ┌────────────────────┐
    │
                - │  │   {{メイングラフ}}   │     │
 {{サブグラフ}}     │     │
                - │
 └────────────────────┘
    └────────────────────┘
    │
                - ├─────────────────────────────────────────────────────────┤
                - │                    詳細テーブル層
                       │
                - │
 ┌─────────────────────────────────────────────────┐
    │
                - │  │            {{アクションテーブル}}
               │     │
                - │
 └─────────────────────────────────────────────────┘
    │
                - └─────────────────────────────────────────────────────────┘
            - kpi_card_templates:
                - alert_kpi:
                    - type: "数値カード"
                    - formula: "COUNTIF({{テーブル}}.{{フィールド}},
'{{危険値}}')"
                    - display: "大きな数字 + アイコン"
                    - color_coding:
                        - - "0: 🟢緑"
                        - - "1-5: 🟡黄"
                        - - "6+: 🔴赤"
                    - click_action: "フィルタービュー表示"
                - financial_kpi:
                    - type: "通貨カード"
                    - formula: "SUMIF({{テーブル}}.{{金額}},
{{条件}})"
                    - display: "通貨形式 + 前期比"
                    - trend: "矢印表示（↑↓→）"
                - percentage_kpi:
                    - type: "パーセントカード"
                    - formula: "{{分子}} / {{分母}} *
100"
                    - display: "ゲージ + 数値"
                    - target_line: "{{目標値}}%"
            - chart_types:
                - bar_chart_vertical:
                    - usage: "カテゴリ別比較、ランキング"
                    - example: "{{カテゴリ}}別{{売上}}"
                - bar_chart_horizontal:
                    - usage: "多項目比較、長い名称"
                    - example: "{{商品}}別{{在庫}}状況"
                - line_chart:
                    - usage: "時系列推移、トレンド"
                    - example: "月別{{指標}}推移"
                - pie_chart:
                    - usage: "構成比、シェア"
                    - example: "{{チャネル}}別売上構成"
                - scatter_plot:
                    - usage: "相関分析、分布"
                    - example: "{{効率}}×{{収益}}分析"
                - combo_chart:
                    - usage: "複数指標の同時表示"
                    - example: "{{売上}}棒グラフ +
{{利益率}}折れ線"
    - # 権限設定の階層構造
        - permission_hierarchy:
            - levels:
                - admin:
                    - name: "管理者（Admin）"
                    - permissions:
                        - - "全機能へのフルアクセス"
                        - - "システム設定変更"
                        - - "権限管理"
                        - - "データ削除"
                - manager:
                    - name: "マネージャー（Manager）"
                    - permissions:
                        - - "承認権限"
                        - - "レポート作成"
                        - - "部門間データ閲覧"
                        - - "一部設定変更"
                - editor:
                    - name: "編集者（Editor）"
                    - permissions:
                        - - "データ作成・編集"
                        - - "自部門データ管理"
                        - - "ワークフロー実行"
                        - - "エクスポート"
                - contributor:
                    - name: "投稿者（Contributor）"
                    - permissions:
                        - - "データ作成"
                        - - "自分のデータ編集"
                        - - "コメント追加"
                        - - "基本的な閲覧"
                - viewer:
                    - name: "閲覧者（Viewer）"
                    - permissions:
                        - - "データ閲覧のみ"
                        - - "ダウンロード不可"
                        - - "編集不可"
                        - - "コメント閲覧のみ"
            - table_permission_matrix:
                - master_data:
                    - admin: "作成・読取・更新・削除"
                    - manager: "読取・更新"
                    - editor: "読取・更新（{{制限フィールド}}除く）"
                    - contributor: "読取のみ"
                    - viewer: "読取のみ（{{機密フィールド}}除く）"
                - transaction_data:
                    - admin: "作成・読取・更新・削除"
                    - manager: "作成・読取・更新・承認"
                    - editor: "作成・読取・更新（自データ）"
                    - contributor: "作成・読取（自データ）"
                    - viewer: "読取のみ（公開データ）"
            - field_level_permissions:
                - sensitive_fields:
                    - cost_price:
                        - display: "管理者、マネージャー、担当編集者"
                        - edit: "管理者のみ"
                    - personal_info:
                        - display: "管理者、担当者"
                        - edit: "管理者のみ"
                    - financial_info:
                        - display: "管理者、財務担当"
                        - edit: "財務担当のみ"
    - # 効果測定指標テンプレート
        - measurement_metrics_template:
            - immediate_metrics:
                - time_reduction:
                    - search_work: "{{現状}}分 → {{改善後}}秒（{{削減率}}%削減）"
                    - input_work: "{{現状}}分 → {{改善後}}分（{{削減率}}%削減）"
                    - verification_work: "{{現状}}分 →
{{改善後}}秒（{{削減率}}%削減）"
                - error_reduction:
                    - input_errors: "{{現状}}% → {{改善後}}%（{{改善率}}%改善）"
                    - processing_omissions: "{{現状}}%
→ {{改善後}}%（{{改善率}}%改善）"
                - automation_rate:
                    - process1: "手動 → {{自動化率}}%自動化"
                    - process2: "{{現状}}% → {{改善後}}%自動化"
            - long_term_metrics:
                - operational_efficiency:
                    - monthly_processing_time: "{{現状}}時間
→ {{改善後}}時間"
                    - lead_time: "{{現状}}日 → {{改善後}}日"
                    - processing_capacity: "{{現状}}件/日
→ {{改善後}}件/日"
                - quality_improvement:
                    - accuracy: "{{現状}}% → {{目標}}%"
                    - satisfaction: "{{現状}}点 → {{目標}}点"
                    - compliance: "{{現状}}% → {{目標}}%"
                - financial_impact:
                    - labor_cost_reduction: "年間{{金額}}万円"
                    - opportunity_loss_reduction: "年間{{金額}}万円"
                    - total_cost_reduction: "年間{{金額}}万円"
                    - roi: "{{回収期間}}ヶ月で回収"
    - # Lark MCP操作マニュアル（YAML形式）
        - lark_mcp_operation_manual:
            - title: "Lark MCP操作 - 絶対に間違えないインストラクション"
            - critical_lessons:
                - common_errors:
                    - - error_type: "app_token混同エラー"
                        - description: "WikiノードトークンとBitableトークンを混同"
                    - - error_type:
"FieldNameNotFound"
                        - description: "フィールド名の不正確な指定"
                    - - error_type: "API順序エラー"
                        - description: "適切な手順を踏まない操作"
            - mandatory_operation_steps:
                - step1_wiki_child_token:
                    - title: "Wikiチャイルド用app_token取得（WikiのBitableの場合）"
                    - required_when: "WikiチャイルドBitableの場合"
                    - procedure:
                        - - action:
"wiki_v2_space_getNodeを実行"
                        - - action: "obj_tokenを取得"
                        - - action: "これがBitableのapp_token"
                    - warning:
                        - wrong: "Wikiのnode_tokenをapp_tokenとして使用"
                        - correct: "wiki APIでobj_tokenを取得してからBitable
APIを使用"
                    - code_example: |
                        - // Step 1: Wiki APIでobj_token取得
                        - lark-mcp:wiki_v2_space_getNode
                        - params: {"token": "Wikiのノードトークン"}
                        - // レスポンスからobj_tokenを取得
                        - "obj_token":
"W66tbCpb7avIjSsGvBhjRxtZpHc"
← これがapp_token
                - step2_table_list:
                    - title: "テーブル一覧取得（必須）"
                    - code_example: |
                        - // Step 2: テーブル一覧取得
                        - lark-mcp:bitable_v1_appTable_list
                        - params: {"page_size": 20}
                        - path: {"app_token": "Step1で取得したobj_token"}
                        - useUAT: true
                - step3_field_list:
                    - title: "フィールド一覧取得（必須）"
                    - code_example: |
                        - // Step 3: 各テーブルのフィールド詳細取得
                        - lark-mcp:bitable_v1_appTableField_list
                        - params: {"page_size": 50}
                        - path: {"table_id": "tblXXXXXX",
"app_token": "obj_token"}
                        - useUAT: true
                    - important_note: "この結果の'field_name'を正確にコピーして使用"
                - step4_record_operations:
                    - title: "レコード操作（正確なフィールド名使用）"
                    - operations:
                        - search:
                            - title: "レコード検索"
                            - code_example: |
                                - lark-mcp:bitable_v1_appTableRecord_search
                                - data: {"automatic_fields":
true}  // 全フィールド取得
                                - params: {"page_size": 10,
"user_id_type": "open_id"}
                                - path: {"table_id":
"tblXXXXXX", "app_token":
"obj_token"}
                                - useUAT: true
                        - create:
                            - title: "レコード作成"
                            - code_example: |
                                - lark-mcp:bitable_v1_appTableRecord_create
                                - data: {"fields": {"正確なフィールド名":
"値"}}
                                - params: {"user_id_type":
"open_id"}
                                - path: {"table_id":
"tblXXXXXX", "app_token":
"obj_token"}
                                - useUAT: true
                        - update:
                            - title: "レコード更新"
                            - code_example: |
                                - lark-mcp:bitable_v1_appTableRecord_update
                                - data: {"fields": {"正確なフィールド名":
"値"}}
                                - params: {"user_id_type":
"open_id"}
                                - path: {"table_id":
"tblXXXXXX", "app_token":
"obj_token", "record_id":
"recXXXXXX"}
                                - useUAT: true
            - absolute_rules:
                - rule1_token_management:
                    - title: "Token管理"
                    - prohibited:
                        - - "WikiのノードトークンをBitableのapp_tokenとして使用"
                        - - "推測でトークンを指定"
                    - required:
                        - - "wiki_v2_space_getNodeでobj_token取得"
                        - - "obj_tokenをapp_tokenとして使用"
                        - - "エラーが発生したら再度obj_token確認"
                - rule2_field_name_management:
                    - title: "フィールド名管理"
                    - prohibited:
                        - - "推測でフィールド名を指定"
                        - - "部分的なフィールド名を使用"
                        - - "絵文字の有無を適当に判断"
                    - required:
                        - - "bitable_v1_appTableField_listでフィールド一覧取得"
                        - - "'field_name'を正確にコピー&ペースト"
                        - - "エスケープ文字も含めて完全一致で使用"
                - rule3_error_handling:
                    - title: "エラー処理"
                    - field_name_not_found:
                        - - "即座にbitable_v1_appTableField_listを再実行"
                        - - "正確なフィールド名を確認"
                        - - "完全一致で再試行"
                    - not_exist_error:
                        - - "app_tokenが正しいか確認"
                        - - "WikiチャイルドBitableの場合はwiki
APIで再取得"
                        - - "table_idが正しいか確認"
            - standard_operation_flow:
                - new_project:
                    - title: "新しいプロジェクト開始時"
                    - steps:
                        - - "wiki_v2_space_getNode →
obj_token取得"
                        - - "bitable_v1_appTable_list →
テーブル一覧確認"
                        - - "各テーブルでbitable_v1_appTableField_list
→ フィールド確認"
                        - -
"bitable_v1_appTableRecord_search
→ データ確認"
                        - - "必要に応じてレコード操作"
                - continuous_work:
                    - title: "継続作業時"
                    - steps:
                        - - "前回のobj_tokenが有効か確認"
                        - - "エラーが発生したらStep 1から再実行"
                        - - "フィールド名は必ず最新情報で確認"
            - best_practices:
                - information_storage:
                    - title: "情報の保存"
                    - items:
                        - - "obj_token (app_token)"
                        - - "table_id一覧"
                        - - "各テーブルのfield_name一覧"
                        - - "重要なrecord_id"
                - error_prevention:
                    - title: "エラー予防"
                    - checklist:
                        - - "app_tokenが正しい（obj_token）"
                        - - "table_idが正しい"
                        - - "field_nameが正確（完全一致）"
                        - - "useUAT: trueが設定されている"
                - debug_procedure:
                    - title: "デバッグ手順"
                    - steps:
                        - - step: "エラーメッセージの種類を確認"
                            - details:
                                - - "NOTEXIST → token/ID確認"
                                - - "FieldNameNotFound → フィールド名確認"
                        - - step: "基本的な接続テスト（appTable_list）"
                        - - step: "フィールド情報の再取得"
                        - - step: "最小限のデータで再試行"
            - implementation_checklist:
                - before_start:
                    - - "WikiチャイルドBitableの場合は
wiki API を使用"
                    - - "obj_token を正確に取得"
                    - - "テーブル一覧を確認"
                    - - "フィールド一覧を確認"
                - during_operation:
                    - - "app_token が obj_token と一致"
                    - - "field_name が完全一致"
                    - - "useUAT: true が設定"
                    - - "エラー時は基本接続から確認"
                - after_completion:
                    - - "操作が成功"
                    - - "データが正確に反映"
                    - - "関連テーブルとの整合性確認"
            - efficiency_metrics:
                - improvements:
                    - - metric: "エラー発生率"
                        - improvement: "90%削減"
                    - - metric: "デバッグ時間"
                        - improvement: "80%短縮"
                    - - metric: "作業効率"
                        - improvement: "3倍向上"
        - # 主キー設計の標準原則
            - primary_key_design:
                - title: "主キー設計の標準原則"
                - description: "Lark Baseにおける効果的な主キー設計とリレーション最適化"
                - core_principles:
                    - bidirectional_first:
                        - principle: "全てのリレーションは双方向リンクを基本とする"
                        - reason: "データの可視性と追跡性を最大化"
                    - visibility_optimization:
                        - principle: "リレーション先テーブルでレコード内容が識別可能にする"
                        - reason: "レコード詳細を開かずに内容を把握可能"
                    - leftmost_positioning:
                        - principle: "主キーフィールドは常にテーブルの最左端に配置"
                        - reason: "全体像の即座の把握を可能にする"
                - field_patterns:
                    - #
==========================================
                    - # パターン1: 直接入力型主キー
                    - #
==========================================
                    - direct_input_pattern:
                        - usage: "マスターデータ、固定的な識別子"
                        - examples:
                            - - field: "{{取引先名}}"
                                - type: "テキスト"
                                - format: "株式会社○○"
                                - position: "最左端"
                            - - field: "{{担当者名}}"
                                - type: "テキスト"
                                - format: "山田太郎"
                                - position: "最左端"
                            - - field: "{{商品コード}}"
                                - type: "テキスト"
                                - format: "PRD-12345"
                                - position: "最左端"
                    - #
==========================================
                    - # パターン2: 数式結合型主キー
                    - #
==========================================
                    - formula_composite_pattern:
                        - usage: "トランザクションデータ、動的な識別子"
                        - standard_formulas:
                            - date_prefix_pattern:
                                - description: "日付を先頭に配置するパターン"
                                - formula: |
                                    - CONCATENATE(
                                        - TEXT({{日付フィールド}},
"YYYY-MM-DD"),
                                        - "_",
                                        - {{取引先名}},
                                        - "_",
                                        - {{案件種別}}
                                    - )
                                - example_output: "2024-01-15_株式会社ABC_定期発注"
                            - status_prefix_pattern:
                                - description: "ステータスを先頭に配置するパターン"
                                - formula: |
                                    - CONCATENATE(
                                        - "[", {{ステータス}}, "]",
                                        - TEXT({{日付}}, "YYMMDD"),
                                        - "_",
                                        - {{顧客名}},
                                        - "_",
                                        - {{概要}}
                                    - )
                                - example_output: "[完了]240115_山田商事_システム導入"
                            - sequential_number_pattern:
                                - description: "連番を含むパターン"
                                - formula: |
                                    - CONCATENATE(
                                        - {{プレフィックス}},
                                        - "-",
                                        - TEXT({{作成日}},
"YYYYMM"),
                                        - "-",
                                        - TEXT({{連番}}, "0000")
                                    - )
                                - example_output: "ORD-202401-0042"
                - implementation_rules:
                    - #
==========================================
                    - # テーブル別実装ルール
                    - #
==========================================
                    - master_tables:
                        - rule: "直接入力型を使用"
                        - fields:
                            - - "{{会社名}} - 最左端配置、必須、ユニーク制約"
                            - - "{{従業員名}} - 最左端配置、必須"
                            - - "{{製品名}} - 最左端配置、必須、ユニーク制約"
                    - transaction_tables:
                        - rule: "数式結合型を使用"
                        - fields:
                            - daily_report:
                                - name: "{{日報ID}}"
                                - formula: |
                                    - CONCATENATE(
                                        - TEXT({{報告日}}, "YYYY-MM-DD"),
                                        - "_",
                                        - {{担当者名}},
                                        - "_",
                                        - LEFT({{業務内容}}, 20)
                                    - )
                                - example: "2024-01-15_田中太郎_営業訪問（A社定期MTG）"
                            - task_management:
                                - name: "{{タスクID}}"
                                - formula: |
                                    - CONCATENATE(
                                        - "[", {{優先度}}, "]",
                                        - TEXT({{期限}}, "MM/DD"),
                                        - "_",
                                        - {{プロジェクト名}},
                                        - "_",
                                        - {{タスク名}}
                                    - )
                                - example: "[高]01/20_新システム開発_要件定義書作成"
                            - order_management:
                                - name: "{{注文ID}}"
                                - formula: |
                                    - CONCATENATE(
                                        - "ORD-",
                                        - TEXT({{注文日}},
"YYMMDD"),
                                        - "-",
                                        - {{顧客コード}},
                                        - "-",
                                        - TEXT({{注文番号}}, "000")
                                    - )
                                - example: "ORD-240115-CUS001-042"
                - visibility_enhancement:
                    - #
==========================================
                    - # 可視性向上のための追加設定
                    - #
==========================================
                    - lookup_fields:
                        - description: "関連テーブルの重要情報を表示"
                        - implementation:
                            - - source: "{{取引先}}"
                                - lookups:
                                    - - "{{最終取引日}}"
                                    - - "{{取引額累計}}"
                                    - - "{{担当営業}}"
                            - - source: "{{商品}}"
                                - lookups:
                                    - - "{{在庫数}}"
                                    - - "{{単価}}"
                                    - - "{{カテゴリ}}"
                    - preview_fields:
                        - description: "リンクフィールドのプレビュー設定"
                        - settings:
                            - - display_fields: 3  # 最大3フィールドを表示
                            - - priority_order:
                                - 1. "主キー（ID）"
                                - 2. "ステータス"
                                - 3. "金額または数量"
                - best_practices:
                    - #
==========================================
                    - # ベストプラクティス
                    - #
==========================================
                    - naming_conventions:
                        - - prefix_usage:
                            - 目的: "データの分類と検索性向上"
                            - examples:
                                - - "CUS- : 顧客関連"
                                - - "ORD- : 注文関連"
                                - - "TSK- : タスク関連"
                                - - "RPT- : レポート関連"
                        - - date_format:
                            - 推奨: "YYYY-MM-DD（ソート最適化）"
                            - 代替: "YYMMDD（文字数削減）"
                        - - separator:
                            - 推奨: "_（アンダースコア）"
                            - 理由: "可読性とコピペ時の利便性"
                    - length_optimization:
                        - max_length: 100  # 文字数上限
                        - truncation_rules:
                            - - "説明文は20文字でLEFT()関数で切り取り"
                            - - "重要な識別情報を前方に配置"
                            - - "省略可能な情報は後方に配置"
    - 会社情報
        - KPI設定の数字の強弱
            - User Input
        - 会社ホームページURL
            - https://larkdx.com/#feature
 - # コマンドスタック実装
    - command_stack:
        - #
==================================
        - # C1: システム構造分析・設計
        - #
==================================
        - C1_system_analysis:
            - description: "システム要件を分析し、Lark
Baseの構造に落とし込む"
            - tasks:
                - T1_requirement_definition:
                    - prompt: |
                        - 以下の項目を具体的に定義してください：
                        - - アプリケーション名: {{業界}}{{業務領域}}統合管理システム
                        - - 主要業務: {{主要業務1}}, {{主要業務2}},
{{主要業務3}}
                        - - 利用者数: {{最小利用者数}}-{{最大利用者数}}名
                        - - 管理対象数: {{初期数}}+（継続増加見込み）
                        - - 取引先数: {{取引先数}}社
                        - - チャネル数: {{チャネル数}}
                        - - 月間処理件数: {{最小処理数}}-{{最大処理数}}件
                    - output:
"requirement_spec.yaml"
                - T2_data_structure_design:
                    - prompt: |
                        - 以下のテーブル構造を設計してください：
                        - 1. マスターテーブル（静的データ）
                            - - {{商品/サービス}}マスタ
                            - - {{取引先}}マスタ
                            - - {{カテゴリ}}マスタ
                        - 2. トランザクションテーブル（動的データ）
                            - - {{注文/依頼}}テーブル
                            - - {{処理/作業}}テーブル
                            - - {{履歴}}テーブル
                        - 3. 関連テーブル
                            - - {{分析用}}テーブル
                            - - {{設定}}テーブル
                    - output: "table_design.yaml"
        - #
==================================
        - # C2: フィールド設計・実装
        - #
==================================
        - C2_field_implementation:
            - description: "各テーブルのフィールドを詳細設計・実装"
            - tasks:
                - T0_primary_key_setup:  # 新規追加タスク
                    - prompt: |
                        - 各テーブルの主キーフィールドを設計・実装してください：
                        - 1. {{マスターテーブル}}の主キー設定
                            - - フィールド名: {{エンティティ名}}
                            - - タイプ: テキスト（直接入力）
                            - - 位置: 最左端
                            - - 制約: 必須、ユニーク
                        - 2. {{トランザクションテーブル}}の主キー設定
                            - - フィールド名: {{トランザクションID}}
                            - - タイプ: 数式
                            - - 数式:
                                - CONCATENATE(
                                    - TEXT({{日付}}, "YYYY-MM-DD"),
                                    - "_",
                                    - {{関連エンティティ}},
                                    - "_",
                                    - LEFT({{説明}}, 20)
                                - )
                            - - 位置: 最左端
                            - - 表示例: "2024-01-15_ABC商事_定期メンテナンス実施"
                        - 3. プレビュー設定
                            - - 各リンクフィールドで表示する情報を3つまで選択
                            - - 優先順位: ID > ステータス
> 金額/数量
                    - output:
"primary_key_design.json"
                    - priority: "最優先（他フィールド作成前に実行）"
                - T1_master_fields:
                    - prompt: |
                        - {{マスタテーブル名}}に以下のフィールドを作成してください：
                        - - ID（テキスト/自動採番）:
{{ID形式}}
                        - - 名称（テキスト）: {{名称}}
                        - - カテゴリ（単一選択）:
                            - 選択肢: {{カテゴリ1}}, {{カテゴリ2}},
{{カテゴリ3}}
                            - 色: 標準色パレット使用（1行目の色）
                        - - ステータス（単一選択）:
                            - - 有効: 🟢緑（1行目5番目）
                            - - 無効: 🤍グレー（1行目11番目）
                        - - 数値データ（数値/通貨）:
{{単価}}, {{在庫数}}
                        - - 日付（日付）: {{登録日}},
{{更新日}}
                        - - 担当者（ユーザー）: 単一選択
                        - - 備考（テキスト）: 複数行
                    - output: "master_fields.json"
                - T2_transaction_fields:
                    - prompt: |
                        - {{トランザクションテーブル名}}に以下のフィールドを作成してください：
                        - - 処理番号（自動採番）: {{プレフィックス}}-YYYYMMDD-0001形式
                        - - ステータス（単一選択）:
                            - - 新規: 🔵青
                            - - 処理中: 🟡黄
                            - - 完了: 🟢緑
                            - - キャンセル: 🤍グレー
                            - - エラー: ❤️赤
                        - - 優先度（単一選択）:
                            - - 緊急: ❤️赤
                            - - 高: 🟡黄
                            - - 中: 🔵青
                            - - 低: 🤍グレー
                        - - 金額関連（通貨）: {{金額}},
{{税額}}, {{合計}}
                        - - 期日（日付）: {{開始日}},
{{期限}}, {{完了日}}
                        - - フラグ（チェックボックス）:
{{緊急フラグ}}, {{承認フラグ}}
                    - output:
"transaction_fields.json"
                - T3_formula_fields:
                    - prompt: |
                        - 以下の数式フィールドを作成してください：
                        - 1. 残日数計算:
                            - IF({{ステータス}} != "完了",
{{期限}} - TODAY(), "完了済")
                        - 2. 在庫予測:
                            - IF({{在庫}} / {{日次平均}} <
7, "🚨緊急発注",
                            - IF({{在庫}} / {{日次平均}} <
14, "⚠️要確認", "✅正常"))
                        - 3. 達成率:
                            - IF({{目標}} > 0, {{実績}} /
{{目標}} * 100, 0)
                        - 4. アラート判定:
                            - IF({{残日数}} < 0, "遅延",
                            - IF({{残日数}} < 3, "期限間近",
"正常"))
                    - output: "formula_fields.json"
        - #
==================================
        - # C3: リレーション構築
        - #
==================================
        - C3_relation_setup:
            - description: "テーブル間の双方向リンクを設定"
            - tasks:
                - T0_visibility_check:  # 新規追加タスク
                    - prompt: |
                        - リレーション設定後の可視性を確認：
                        - 1. 双方向リンクの表示確認
                            - - 親テーブル側: 関連レコード数の表示
                            - - 子テーブル側: 親レコードの主要情報表示
                        - 2. ルックアップフィールドの追加
                            - - {{取引先}}から: 最終取引日、累計金額
                            - - {{商品}}から: 在庫数、単価
                            - - {{プロジェクト}}から: 進捗率、期限
                        - 3. リンクプレビューの最適化
                            - - 表示フィールド数: 3
                            - - 表示順序の調整
                    - output:
"visibility_optimization.json"
                    - priority: "リレーション設定直後に実行"
                - T1_prepare_tables:
                    - prompt: |
                        - リレーション設定前の準備：
                        - 1. 全テーブルが作成完了していることを確認
                        - 2. 各テーブルに主キーフィールドを設定
                        - 3. リレーション設定順序を決定（子
→親の順）
                    - output:
"relation_preparation.yaml"
                - T2_create_links:
                    - prompt: |
                        - 以下の双方向リンクを作成してください：
                        - 1. {{注文}}→{{商品}}マスタ（多:1）
                            - - フィールド名: {{商品名}}
                            - - 参照テーブル: {{商品}}マスタ
                            - - 参照フィールド: {{商品ID}}
                            - - 選択可能数: 単一
                        - 2. {{注文}}→{{取引先}}マスタ（多:1）
                            - - フィールド名: {{取引先名}}
                            - - 参照テーブル: {{取引先}}マスタ
                            - - 参照フィールド: {{取引先ID}}
                            - - 選択可能数: 単一
                        - 3. {{タスク}}→{{プロジェクト}}（多:多）
                            - - フィールド名: {{関連プロジェクト}}
                            - - 参照テーブル: {{プロジェクト}}
                            - - 選択可能数: 複数
                    - output:
"bidirectional_links.json"
                - T3_create_lookups:
                    - prompt: |
                        - リンクを使用したルックアップフィールドを作成：
                        - 1. {{商品単価}}（ルックアップ）
                            - - 参照: {{商品}}.{{単価}}
                        - 2. {{取引先情報}}（ルックアップ）
                            - - 参照: {{取引先}}.{{連絡先}}
                        - 3. {{関連集計}}（ルックアップ＋集計）
                            - - 参照: SUM({{関連レコード}}.{{金額}})
                    - output: "lookup_fields.json"
        - #
==================================
        - # C4: ワークフロー実装
        - #
==================================
        - C4_workflow_automation:
            - description: "自動化ワークフローを構築"
            - tasks:
                - T1_alert_workflows:
                    - prompt: |
                        - {{在庫切れ予測アラート}}ワークフローを作成：
                        - - トリガー: 定期実行（毎日
09:00）
                        - - 対象: {{商品}}マスタ
                        - - 条件: {{在庫予測}} < 7
                        - - アクション:
                            - 1. {{アラートステータス}} = "
🚨要対応"
                            - 2. 通知: @{{担当者}}に「{{商品名}}の在庫が残り{{在庫予測}}日です」
                            - 3. タスク作成: {{発注タスク}}テーブルに新規レコード
                    - output: "alert_workflow.json"
                - T2_approval_workflows:
                    - prompt: |
                        - {{金額承認}}ワークフローを作成：
                        - - トリガー: {{ステータス}} =
"承認申請"
                        - - 条件: {{金額}} >= {{承認必要金額}}
                        - - アクション:
                            - 1. 承認リクエスト送信
                                - - 承認者: {{承認者フィールド}}
                                - - 期限: 3営業日
                            - 2. 承認時: {{ステータス}} =
"承認済", {{承認日}} = TODAY()
                            - 3. 否認時: {{ステータス}} =
"差戻し", 通知送信
                            - 4. リマインダー: 1日後未承認なら再通知
                    - output:
"approval_workflow.json"
                - T3_process_workflows:
                    - prompt: |
                        - {{自動処理}}ワークフローを作成：
                        - - トリガー: {{実績入力}}フィールド更新時
                        - - アクション:
                            - 1. 関連レコード更新
                                - - {{在庫}} = {{在庫}} - {{出荷数}}
                            - 2. ステータス更新
                                - - {{処理ステータス}} = "完了"
                                - - {{完了日}} = TODAY()
                            - 3. 次工程開始
                                - - {{次工程テーブル}}に新規レコード作成
                                - - 初期値設定
                    - output:
"process_workflow.json"
        - #
==================================
        - # C5: ボタン実装
        - #
==================================
        - C5_button_implementation:
            - description: "アクションボタンを設定"
            - tasks:
                - T1_quick_create_buttons:
                    - prompt: |
                        - 🚀{{簡易作成}}ボタンを実装：
                        - 1. 配置: {{メインテーブル}}の各レコード
                        - 2. アクション:
                            - - 現在のレコード情報を取得
                            - - {{関連テーブル}}に新規レコード作成
                            - - デフォルト値を自動設定
                            - - 作成完了通知表示
                        - 3. 表示条件: {{ステータス}} =
"{{対象ステータス}}"
                    - output:
"quick_create_button.json"
                - T2_external_link_buttons:
                    - prompt: |
                        - 📞{{外部連携}}ボタンを実装：
                        - 1. 連絡先情報の取得
                        - 2. 外部アプリケーション起動
                            - - URL: {{アプリスキーム}}://{{パラメータ}}
                        - 3. 連絡履歴の自動記録
                        - 4. 結果の更新
                    - output:
"external_link_button.json"
                - T3_batch_process_buttons:
                    - prompt: |
                        - 📊{{一括処理}}ボタンを実装：
                        - 1. 対象レコードの特定
                            - - 条件: {{フィルター条件}}
                        - 2. 一括更新実行
                            - - {{ステータス}}更新
                            - - {{処理日}}記録
                        - 3. 処理結果の集計
                        - 4. 完了通知
                    - output:
"batch_process_button.json"
        - #
==================================
        - # C6: ビュー作成
        - #
==================================
        - C6_view_creation:
            - description: "各種ビューを作成・設定"
            - tasks:
                - T1_grid_views:
                    - prompt: |
                        - {{業務別}}グリッドビューを作成：
                        - 1. {{管理者用}}ビュー
                            - - 全フィールド表示
                            - - フィルター: なし
                            - - ソート: {{優先度}}降順,
{{期日}}昇順
                        - 2. {{担当者用}}ビュー
                            - - 表示: 必要フィールドのみ
                            - - フィルター: {{担当者}} =
CURRENT_USER()
                            - - 条件付き書式: {{期限}}による色分け
                        - 3. {{分析用}}ビュー
                            - - グループ化: {{カテゴリ}}
                            - - 集計行表示
                    - output: "grid_views.json"
                - T2_kanban_views:
                    - prompt: |
                        - {{プロセス管理}}カンバンビューを作成：
                        - - グループ化: {{ステータス}}
                        - - カード表示:
                            - - タイトル: {{案件名}}
                            - - サブ情報: {{担当者}}, {{期限}}
                            - - タグ: {{優先度}}, {{カテゴリ}}
                        - - 色分け: {{緊急度}}
                        - - WIP制限: 各列最大{{制限数}}件
                    - output: "kanban_views.json"
                - T3_calendar_views:
                    - prompt: |
                        - {{スケジュール}}カレンダービューを作成：
                        - - 日付フィールド: {{予定日}}
                        - - イベント表示:
                            - - {{タイトル}}
                            - - {{詳細情報}}
                        - - 色分け: {{種別}}による自動色分け
                        - - フィルター: {{有効フラグ}}
= true
                    - output: "calendar_views.json"
        - #
==================================
        - # C7: ダッシュボード構築
        - #
==================================
        - C7_dashboard_creation:
            - description: "分析ダッシュボードを構築"
            - tasks:
                - T1_kpi_cards:
                    - prompt: |
                        - KPIカードを作成（上部4枚）：
                        - 1. 🚨{{緊急対応件数}}
                            - - 数式: COUNTIF({{ステータス}},
"緊急")
                            - - 色分け: 0=緑, 1-5=黄, 6+=赤
                        - 2. 💰{{本日売上}}
                            - - 数式: SUMIF({{日付}},
TODAY())
                            - - 前日比表示
                        - 3. 📈{{達成率}}
                            - - 数式: {{実績}}/{{目標}}*100
                            - - ゲージ表示
                        - 4. ⏱️{{平均処理時間}}
                            - - 数式: AVG({{完了日}}-{{開始日}})
                            - - トレンド矢印
                    - output: "kpi_cards.json"
                - T2_main_charts:
                    - prompt: |
                        - メイングラフを作成：
                        - 1. {{月別推移}}折れ線グラフ
                            - - X軸: 月
                            - - Y軸: {{売上}}, {{利益}}（複合）
                        - 2. {{カテゴリ別}}棒グラフ
                            - - 降順ソート
                            - - TOP10表示
                        - 3. {{構成比}}円グラフ
                            - - {{チャネル}}別売上構成
                    - output: "main_charts.json"
                - T3_action_tables:
                    - prompt: |
                        - アクションテーブルを作成：
                        - - 名称: {{要対応リスト}}
                        - - フィルター: {{ステータス}}
IN ("緊急", "要確認")
                        - - 表示項目: {{案件名}}, {{期限}},
{{担当者}}, {{アクション}}
                        - - ソート: {{優先度}}降順, {{期限}}昇順
                        - - アクション: 各行にボタン配置
                    - output: "action_tables.json"
        - #
==================================
        - # C8: 権限設定
        - #
==================================
        - C8_permission_setup:
            - description: "階層的な権限を設定"
            - tasks:
                - T1_role_definition:
                    - prompt: |
                        - 5段階の権限ロールを定義：
                        - 1. 管理者（Admin）
                            - - 全機能フルアクセス
                            - - システム設定変更
                            - - 権限管理
                        - 2. マネージャー（Manager）
                            - - 承認権限
                            - - レポート作成
                            - - 部門間データ閲覧
                        - 3. 編集者（Editor）
                            - - データ作成・編集
                            - - 自部門データ管理
                        - 4. 投稿者（Contributor）
                            - - データ作成
                            - - 自分のデータ編集
                        - 5. 閲覧者（Viewer）
                            - - データ閲覧のみ
                    - output: "role_definition.yaml"
                - T2_table_permissions:
                    - prompt: |
                        - テーブル別権限マトリックスを設定：
                        - - {{マスターデータ}}:
                            - - Admin: CRUD全権限
                            - - Manager: 読取・更新
                            - - Editor: 読取・更新（制限付き）
                            - - Contributor: 読取のみ
                            - - Viewer: 読取のみ（機密除く）
                        - - {{トランザクション}}:
                            - - Admin: CRUD全権限
                            - - Manager: CRU+承認
                            - - Editor: CRU（自データ）
                            - - Contributor: CR（自データ）
                            - - Viewer: R（公開データ）
                    - output:
"table_permissions.json"
                - T3_field_permissions:
                    - prompt: |
                        - フィールドレベル権限を設定：
                        - 1. {{原価・仕入値}}
                            - - 表示: Admin, Manager, 担当Editor
                            - - 編集: Adminのみ
                        - 2. {{個人情報}}
                            - - 表示: Admin, 担当者
                            - - 編集: Adminのみ
                        - 3. {{財務情報}}
                            - - 表示: Admin, 財務担当
                            - - 編集: 財務担当のみ
                    - output:
"field_permissions.json"
        - #
==================================
        - # C9: テスト・検証
        - #
==================================
        - C9_testing_validation:
            - description: "システムの動作確認と検証"
            - tasks:
                - T1_unit_testing:
                    - prompt: |
                        - 各機能の単体テスト：
                        - □ フィールド計算の正確性
                        - □ リンクの参照整合性
                        - □ ワークフローの動作
                        - □ ボタンアクションの実行
                        - □ 権限による制御
                    - output: "unit_test_results.yaml"
                - T2_integration_testing:
                    - prompt: |
                        - 統合テストの実施：
                        - □ エンドツーエンドのプロセステスト
                        - □ データフローの確認
                        - □ 通知・アラートの動作
                        - □ ダッシュボードの更新
                        - □ モバイル表示の確認
                    - output:
"integration_test_results.yaml"
                - T3_performance_testing:
                    - prompt: |
                        - パフォーマンステスト：
                        - □ 大量データでの表示速度
                        - □ 複雑な数式の計算時間
                        - □ ワークフローの処理速度
                        - □ 同時アクセス時の安定性
                        - 目標: {{レコード数}}件で{{応答時間}}秒以内
                    - output:
"performance_test_results.yaml"
        - #
==================================
        - # C10: デプロイ・移行
        - #
==================================
        - C10_deployment:
            - description: "本番環境への展開"
            - tasks:
                - T1_data_migration:
                    - prompt: |
                        - 既存データの移行：
                        - 1. データクレンジング
                        - 2. マスターデータのインポート
                        - 3. トランザクションデータの移行
                        - 4. データ整合性の確認
                        - 5. 移行ログの記録
                    - output: "migration_log.yaml"
                - T2_user_setup:
                    - prompt: |
                        - ユーザー設定：
                        - 1. ユーザーアカウントの作成
                        - 2. 権限グループへの割り当て
                        - 3. 初期パスワードの設定
                        - 4. 通知設定の構成
                        - 5. トレーニング資料の配布
                    - output:
"user_setup_complete.yaml"
                - T3_go_live:
                    - prompt: |
                        - 本番稼働：
                        - 1. 最終動作確認
                        - 2. バックアップ設定
                        - 3. 監視アラート設定
                        - 4. ユーザーへの通知
                        - 5. サポート体制の確立
                    - output:
"go_live_checklist.yaml"
 - # 実行コマンド
    - execution:
        - full_implementation: |
            - [成果物: {{業界}}{{業務領域}}統合管理システム]
            - C1 -> C2 -> C3 -> C4 -> C5 ->
C6 -> C7 -> C8 -> C9 -> C10
            - All Run (Sequential)
        - phase_implementation: |
            - Phase 1 (基盤): C1 -> C2 -> C3
            - Phase 2 (自動化): C4 -> C5
            - Phase 3 (最適化): C6 -> C7
            - Phase 4 (運用): C8 -> C9 -> C10
        - parallel_tracks: |
            - Track A: C1 -> C2 -> C3 (データ基盤)
            - Track B: C4 -> C5 (自動化) [After
C2]
            - Track C: C6 -> C7 (可視化) [After
C3]
            - Track D: C8 -> C9 -> C10 (運用準備)
[After C7]
 - # 実装チェックリスト
    - implementation_checklist_master:
        - primary_key_checklist:
            - - "□ 全テーブルの主キーフィールドが最左端に配置されている"
            - - "□ マスターテーブルは直接入力型主キーを使用"
            - - "□ トランザクションテーブルは数式結合型主キーを使用"
            - - "□ 主キーに日付情報が含まれる場合はYYYY-MM-DD形式"
            - - "□ 数式結合の区切り文字は'_'で統一"
            - - "□ 説明文の切り取りは20文字で統一"
            - - "□ リンクフィールドのプレビュー設定完了"
            - - "□ 必要なルックアップフィールドの作成完了"
            - - "□ 全体像が一目で把握できるレイアウト確認"
        - bidirectional_link_checklist:
            - - "□ 全テーブルが作成完了している"
            - - "□ 主キーフィールドが設定されている"
            - - "□ 子テーブルから親テーブルへの参照順序"
            - - "□ 選択可能数（単一/複数）の確認"
            - - "□ 逆方向リンクの自動生成確認"
        - formula_field_checklist:
            - - "□ 参照フィールドの存在確認"
            - - "□ フィールドタイプの一致確認"
            - - "□ ゼロ除算のエラー処理"
            - - "□ NULL値の処理"
            - - "□ 循環参照の回避"
        - workflow_checklist:
            - - "□ トリガー条件の明確化"
            - - "□ 実行条件の論理確認"
            - - "□ アクションの順序性"
            - - "□ エラー時の処理"
            - - "□ 通知先の妥当性"
        - permission_checklist:
            - - "□ 役割の明確な定義"
            - - "□ 最小権限の原則"
            - - "□ 機密フィールドの保護"
            - - "□ 承認フローとの整合性"
            - - "□ 定期的な見直し体制"
 - # 効果測定
    - metrics:
        - immediate:
            - - metric: "作業時間"
                - current: "{{現状}}分"
                - improved: "{{改善後}}秒"
                - reduction: "{{削減率}}%削減"
            - - metric: "エラー率"
                - current: "{{現状}}%"
                - improved: "{{改善後}}%"
                - improvement: "{{改善率}}%改善"
            - - metric: "自動化率"
                - current: "手動"
                - improved: "{{自動化率}}%自動化"
        - long_term:
            - - metric: "処理能力"
                - current: "{{現状}}件/日"
                - improved: "{{改善後}}件/日"
            - - metric: "コスト削減"
                - value: "年間{{金額}}万円"
            - - metric: "ROI"
                - payback_period: "{{回収期間}}ヶ月で投資回収"
 - # コマンドスタック実装
    - command_stack:
        - #
==================================
        - # C1: システム構造分析・設計
        - #
==================================
        - C1_system_analysis:
            - description: "システム要件を分析し、Lark
Baseの構造に落とし込む"
            - tasks:
                - T1_requirement_definition:
                    - prompt: |
                        - 以下の項目を具体的に定義してください：
                        - - アプリケーション名: {{業界}}{{業務領域}}統合管理システム
                        - - 主要業務: {{主要業務1}}, {{主要業務2}},
{{主要業務3}}
                        - - 利用者数: {{最小利用者数}}-{{最大利用者数}}名
                        - - 管理対象数: {{初期数}}+（継続増加見込み）
                        - - 取引先数: {{取引先数}}社
                        - - チャネル数: {{チャネル数}}
                        - - 月間処理件数: {{最小処理数}}-{{最大処理数}}件
                    - output:
"requirement_spec.yaml"
                - T2_data_structure_design:
                    - prompt: |
                        - 以下のテーブル構造を設計してください：
                        - 1. マスターテーブル（静的データ）
                            - - {{商品/サービス}}マスタ
                            - - {{取引先}}マスタ
                            - - {{カテゴリ}}マスタ
                        - 2. トランザクションテーブル（動的データ）
                            - - {{注文/依頼}}テーブル
                            - - {{処理/作業}}テーブル
                            - - {{履歴}}テーブル
                        - 3. 関連テーブル
                            - - {{分析用}}テーブル
                            - - {{設定}}テーブル
                    - output: "table_design.yaml"
        - #
==================================
        - # C2: フィールド設計・実装
        - #
==================================
        - C2_field_implementation:
            - description: "各テーブルのフィールドを詳細設計・実装"
            - tasks:
                - T0_primary_key_setup:  # 新規追加タスク
                    - prompt: |
                        - 各テーブルの主キーフィールドを設計・実装してください：
                        - 1. {{マスターテーブル}}の主キー設定
                            - - フィールド名: {{エンティティ名}}
                            - - タイプ: テキスト（直接入力）
                            - - 位置: 最左端
                            - - 制約: 必須、ユニーク
                        - 2. {{トランザクションテーブル}}の主キー設定
                            - - フィールド名: {{トランザクションID}}
                            - - タイプ: 数式
                            - - 数式:
                                - CONCATENATE(
                                    - TEXT({{日付}}, "YYYY-MM-DD"),
                                    - "_",
                                    - {{関連エンティティ}},
                                    - "_",
                                    - LEFT({{説明}}, 20)
                                - )
                            - - 位置: 最左端
                            - - 表示例: "2024-01-15_ABC商事_定期メンテナンス実施"
                        - 3. プレビュー設定
                            - - 各リンクフィールドで表示する情報を3つまで選択
                            - - 優先順位: ID > ステータス
> 金額/数量
                    - output:
"primary_key_design.json"
                    - priority: "最優先（他フィールド作成前に実行）"
                - T1_master_fields:
                    - prompt: |
                        - {{マスタテーブル名}}に以下のフィールドを作成してください：
                        - - ID（テキスト/自動採番）:
{{ID形式}}
                        - - 名称（テキスト）: {{名称}}
                        - - カテゴリ（単一選択）:
                            - 選択肢: {{カテゴリ1}}, {{カテゴリ2}},
{{カテゴリ3}}
                            - 色: 標準色パレット使用（1行目の色）
                        - - ステータス（単一選択）:
                            - - 有効: 🟢緑（1行目5番目）
                            - - 無効: 🤍グレー（1行目11番目）
                        - - 数値データ（数値/通貨）:
{{単価}}, {{在庫数}}
                        - - 日付（日付）: {{登録日}},
{{更新日}}
                        - - 担当者（ユーザー）: 単一選択
                        - - 備考（テキスト）: 複数行
                    - output: "master_fields.json"
                - T2_transaction_fields:
                    - prompt: |
                        - {{トランザクションテーブル名}}に以下のフィールドを作成してください：
                        - - 処理番号（自動採番）: {{プレフィックス}}-YYYYMMDD-0001形式
                        - - ステータス（単一選択）:
                            - - 新規: 🔵青
                            - - 処理中: 🟡黄
                            - - 完了: 🟢緑
                            - - キャンセル: 🤍グレー
                            - - エラー: ❤️赤
                        - - 優先度（単一選択）:
                            - - 緊急: ❤️赤
                            - - 高: 🟡黄
                            - - 中: 🔵青
                            - - 低: 🤍グレー
                        - - 金額関連（通貨）: {{金額}},
{{税額}}, {{合計}}
                        - - 期日（日付）: {{開始日}},
{{期限}}, {{完了日}}
                        - - フラグ（チェックボックス）:
{{緊急フラグ}}, {{承認フラグ}}
                    - output:
"transaction_fields.json"
                - T3_formula_fields:
                    - prompt: |
                        - 以下の数式フィールドを作成してください：
                        - 1. 残日数計算:
                            - IF({{ステータス}} != "完了",
{{期限}} - TODAY(), "完了済")
                        - 2. 在庫予測:
                            - IF({{在庫}} / {{日次平均}} <
7, "🚨緊急発注",
                            - IF({{在庫}} / {{日次平均}} <
14, "⚠️要確認", "✅正常"))
                        - 3. 達成率:
                            - IF({{目標}} > 0, {{実績}} /
{{目標}} * 100, 0)
                        - 4. アラート判定:
                            - IF({{残日数}} < 0, "遅延",
                            - IF({{残日数}} < 3, "期限間近",
"正常"))
                    - output: "formula_fields.json"
        - #
==================================
        - # C3: リレーション構築
        - #
==================================
        - C3_relation_setup:
            - description: "テーブル間の双方向リンクを設定"
            - tasks:
                - T0_visibility_check:  # 新規追加タスク
                    - prompt: |
                        - リレーション設定後の可視性を確認：
                        - 1. 双方向リンクの表示確認
                            - - 親テーブル側: 関連レコード数の表示
                            - - 子テーブル側: 親レコードの主要情報表示
                        - 2. ルックアップフィールドの追加
                            - - {{取引先}}から: 最終取引日、累計金額
                            - - {{商品}}から: 在庫数、単価
                            - - {{プロジェクト}}から: 進捗率、期限
                        - 3. リンクプレビューの最適化
                            - - 表示フィールド数: 3
                            - - 表示順序の調整
                    - output:
"visibility_optimization.json"
                    - priority: "リレーション設定直後に実行"
                - T1_prepare_tables:
                    - prompt: |
                        - リレーション設定前の準備：
                        - 1. 全テーブルが作成完了していることを確認
                        - 2. 各テーブルに主キーフィールドを設定
                        - 3. リレーション設定順序を決定（子
→親の順）
                    - output:
"relation_preparation.yaml"
                - T2_create_links:
                    - prompt: |
                        - 以下の双方向リンクを作成してください：
                        - 1. {{注文}}→{{商品}}マスタ（多:1）
                            - - フィールド名: {{商品名}}
                            - - 参照テーブル: {{商品}}マスタ
                            - - 参照フィールド: {{商品ID}}
                            - - 選択可能数: 単一
                        - 2. {{注文}}→{{取引先}}マスタ（多:1）
                            - - フィールド名: {{取引先名}}
                            - - 参照テーブル: {{取引先}}マスタ
                            - - 参照フィールド: {{取引先ID}}
                            - - 選択可能数: 単一
                        - 3. {{タスク}}→{{プロジェクト}}（多:多）
                            - - フィールド名: {{関連プロジェクト}}
                            - - 参照テーブル: {{プロジェクト}}
                            - - 選択可能数: 複数
                    - output:
"bidirectional_links.json"
                - T3_create_lookups:
                    - prompt: |
                        - リンクを使用したルックアップフィールドを作成：
                        - 1. {{商品単価}}（ルックアップ）
                            - - 参照: {{商品}}.{{単価}}
                        - 2. {{取引先情報}}（ルックアップ）
                            - - 参照: {{取引先}}.{{連絡先}}
                        - 3. {{関連集計}}（ルックアップ＋集計）
                            - - 参照: SUM({{関連レコード}}.{{金額}})
                    - output: "lookup_fields.json"
        - #
==================================
        - # C4: ワークフロー実装
        - #
==================================
        - C4_workflow_automation:
            - description: "自動化ワークフローを構築"
            - tasks:
                - T1_alert_workflows:
                    - prompt: |
                        - {{在庫切れ予測アラート}}ワークフローを作成：
                        - - トリガー: 定期実行（毎日
09:00）
                        - - 対象: {{商品}}マスタ
                        - - 条件: {{在庫予測}} < 7
                        - - アクション:
                            - 1. {{アラートステータス}} = "
🚨要対応"
                            - 2. 通知: @{{担当者}}に「{{商品名}}の在庫が残り{{在庫予測}}日です」
                            - 3. タスク作成: {{発注タスク}}テーブルに新規レコード
                    - output: "alert_workflow.json"
                - T2_approval_workflows:
                    - prompt: |
                        - {{金額承認}}ワークフローを作成：
                        - - トリガー: {{ステータス}} =
"承認申請"
                        - - 条件: {{金額}} >= {{承認必要金額}}
                        - - アクション:
                            - 1. 承認リクエスト送信
                                - - 承認者: {{承認者フィールド}}
                                - - 期限: 3営業日
                            - 2. 承認時: {{ステータス}} =
"承認済", {{承認日}} = TODAY()
                            - 3. 否認時: {{ステータス}} =
"差戻し", 通知送信
                            - 4. リマインダー: 1日後未承認なら再通知
                    - output:
"approval_workflow.json"
                - T3_process_workflows:
                    - prompt: |
                        - {{自動処理}}ワークフローを作成：
                        - - トリガー: {{実績入力}}フィールド更新時
                        - - アクション:
                            - 1. 関連レコード更新
                                - - {{在庫}} = {{在庫}} - {{出荷数}}
                            - 2. ステータス更新
                                - - {{処理ステータス}} = "完了"
                                - - {{完了日}} = TODAY()
                            - 3. 次工程開始
                                - - {{次工程テーブル}}に新規レコード作成
                                - - 初期値設定
                    - output:
"process_workflow.json"
        - #
==================================
        - # C5: ボタン実装
        - #
==================================
        - C5_button_implementation:
            - description: "アクションボタンを設定"
            - tasks:
                - T1_quick_create_buttons:
                    - prompt: |
                        - 🚀{{簡易作成}}ボタンを実装：
                        - 1. 配置: {{メインテーブル}}の各レコード
                        - 2. アクション:
                            - - 現在のレコード情報を取得
                            - - {{関連テーブル}}に新規レコード作成
                            - - デフォルト値を自動設定
                            - - 作成完了通知表示
                        - 3. 表示条件: {{ステータス}} =
"{{対象ステータス}}"
                    - output:
"quick_create_button.json"
                - T2_external_link_buttons:
                    - prompt: |
                        - 📞{{外部連携}}ボタンを実装：
                        - 1. 連絡先情報の取得
                        - 2. 外部アプリケーション起動
                            - - URL: {{アプリスキーム}}://{{パラメータ}}
                        - 3. 連絡履歴の自動記録
                        - 4. 結果の更新
                    - output:
"external_link_button.json"
                - T3_batch_process_buttons:
                    - prompt: |
                        - 📊{{一括処理}}ボタンを実装：
                        - 1. 対象レコードの特定
                            - - 条件: {{フィルター条件}}
                        - 2. 一括更新実行
                            - - {{ステータス}}更新
                            - - {{処理日}}記録
                        - 3. 処理結果の集計
                        - 4. 完了通知
                    - output:
"batch_process_button.json"
        - #
==================================
        - # C6: ビュー作成
        - #
==================================
        - C6_view_creation:
            - description: "各種ビューを作成・設定"
            - tasks:
                - T1_grid_views:
                    - prompt: |
                        - {{業務別}}グリッドビューを作成：
                        - 1. {{管理者用}}ビュー
                            - - 全フィールド表示
                            - - フィルター: なし
                            - - ソート: {{優先度}}降順,
{{期日}}昇順
                        - 2. {{担当者用}}ビュー
                            - - 表示: 必要フィールドのみ
                            - - フィルター: {{担当者}} =
CURRENT_USER()
                            - - 条件付き書式: {{期限}}による色分け
                        - 3. {{分析用}}ビュー
                            - - グループ化: {{カテゴリ}}
                            - - 集計行表示
                    - output: "grid_views.json"
                - T2_kanban_views:
                    - prompt: |
                        - {{プロセス管理}}カンバンビューを作成：
                        - - グループ化: {{ステータス}}
                        - - カード表示:
                            - - タイトル: {{案件名}}
                            - - サブ情報: {{担当者}}, {{期限}}
                            - - タグ: {{優先度}}, {{カテゴリ}}
                        - - 色分け: {{緊急度}}
                        - - WIP制限: 各列最大{{制限数}}件
                    - output: "kanban_views.json"
                - T3_calendar_views:
                    - prompt: |
                        - {{スケジュール}}カレンダービューを作成：
                        - - 日付フィールド: {{予定日}}
                        - - イベント表示:
                            - - {{タイトル}}
                            - - {{詳細情報}}
                        - - 色分け: {{種別}}による自動色分け
                        - - フィルター: {{有効フラグ}}
= true
                    - output: "calendar_views.json"
        - #
==================================
        - # C7: ダッシュボード構築
        - #
==================================
        - C7_dashboard_creation:
            - description: "分析ダッシュボードを構築"
            - tasks:
                - T1_kpi_cards:
                    - prompt: |
                        - KPIカードを作成（上部4枚）：
                        - 1. 🚨{{緊急対応件数}}
                            - - 数式: COUNTIF({{ステータス}},
"緊急")
                            - - 色分け: 0=緑, 1-5=黄, 6+=赤
                        - 2. 💰{{本日売上}}
                            - - 数式: SUMIF({{日付}},
TODAY())
                            - - 前日比表示
                        - 3. 📈{{達成率}}
                            - - 数式: {{実績}}/{{目標}}*100
                            - - ゲージ表示
                        - 4. ⏱️{{平均処理時間}}
                            - - 数式: AVG({{完了日}}-{{開始日}})
                            - - トレンド矢印
                    - output: "kpi_cards.json"
                - T2_main_charts:
                    - prompt: |
                        - メイングラフを作成：
                        - 1. {{月別推移}}折れ線グラフ
                            - - X軸: 月
                            - - Y軸: {{売上}}, {{利益}}（複合）
                        - 2. {{カテゴリ別}}棒グラフ
                            - - 降順ソート
                            - - TOP10表示
                        - 3. {{構成比}}円グラフ
                            - - {{チャネル}}別売上構成
                    - output: "main_charts.json"
                - T3_action_tables:
                    - prompt: |
                        - アクションテーブルを作成：
                        - - 名称: {{要対応リスト}}
                        - - フィルター: {{ステータス}}
IN ("緊急", "要確認")
                        - - 表示項目: {{案件名}}, {{期限}},
{{担当者}}, {{アクション}}
                        - - ソート: {{優先度}}降順, {{期限}}昇順
                        - - アクション: 各行にボタン配置
                    - output: "action_tables.json"
        - #
==================================
        - # C8: 権限設定
        - #
==================================
        - C8_permission_setup:
            - description: "階層的な権限を設定"
            - tasks:
                - T1_role_definition:
                    - prompt: |
                        - 5段階の権限ロールを定義：
                        - 1. 管理者（Admin）
                            - - 全機能フルアクセス
                            - - システム設定変更
                            - - 権限管理
                        - 2. マネージャー（Manager）
                            - - 承認権限
                            - - レポート作成
                            - - 部門間データ閲覧
                        - 3. 編集者（Editor）
                            - - データ作成・編集
                            - - 自部門データ管理
                        - 4. 投稿者（Contributor）
                            - - データ作成
                            - - 自分のデータ編集
                        - 5. 閲覧者（Viewer）
                            - - データ閲覧のみ
                    - output: "role_definition.yaml"
                - T2_table_permissions:
                    - prompt: |
                        - テーブル別権限マトリックスを設定：
                        - - {{マスターデータ}}:
                            - - Admin: CRUD全権限
                            - - Manager: 読取・更新
                            - - Editor: 読取・更新（制限付き）
                            - - Contributor: 読取のみ
                            - - Viewer: 読取のみ（機密除く）
                        - - {{トランザクション}}:
                            - - Admin: CRUD全権限
                            - - Manager: CRU+承認
                            - - Editor: CRU（自データ）
                            - - Contributor: CR（自データ）
                            - - Viewer: R（公開データ）
                    - output:
"table_permissions.json"
                - T3_field_permissions:
                    - prompt: |
                        - フィールドレベル権限を設定：
                        - 1. {{原価・仕入値}}
                            - - 表示: Admin, Manager, 担当Editor
                            - - 編集: Adminのみ
                        - 2. {{個人情報}}
                            - - 表示: Admin, 担当者
                            - - 編集: Adminのみ
                        - 3. {{財務情報}}
                            - - 表示: Admin, 財務担当
                            - - 編集: 財務担当のみ
                    - output:
"field_permissions.json"
        - #
==================================
        - # C9: テスト・検証
        - #
==================================
        - C9_testing_validation:
            - description: "システムの動作確認と検証"
            - tasks:
                - T1_unit_testing:
                    - prompt: |
                        - 各機能の単体テスト：
                        - □ フィールド計算の正確性
                        - □ リンクの参照整合性
                        - □ ワークフローの動作
                        - □ ボタンアクションの実行
                        - □ 権限による制御
                    - output: "unit_test_results.yaml"
                - T2_integration_testing:
                    - prompt: |
                        - 統合テストの実施：
                        - □ エンドツーエンドのプロセステスト
                        - □ データフローの確認
                        - □ 通知・アラートの動作
                        - □ ダッシュボードの更新
                        - □ モバイル表示の確認
                    - output:
"integration_test_results.yaml"
                - T3_performance_testing:
                    - prompt: |
                        - パフォーマンステスト：
                        - □ 大量データでの表示速度
                        - □ 複雑な数式の計算時間
                        - □ ワークフローの処理速度
                        - □ 同時アクセス時の安定性
                        - 目標: {{レコード数}}件で{{応答時間}}秒以内
                    - output:
"performance_test_results.yaml"
        - #
==================================
        - # C10: デプロイ・移行
        - #
==================================
        - C10_deployment:
            - description: "本番環境への展開"
            - tasks:
                - T1_data_migration:
                    - prompt: |
                        - 既存データの移行：
                        - 1. データクレンジング
                        - 2. マスターデータのインポート
                        - 3. トランザクションデータの移行
                        - 4. データ整合性の確認
                        - 5. 移行ログの記録
                    - output: "migration_log.yaml"
                - T2_user_setup:
                    - prompt: |
                        - ユーザー設定：
                        - 1. ユーザーアカウントの作成
                        - 2. 権限グループへの割り当て
                        - 3. 初期パスワードの設定
                        - 4. 通知設定の構成
                        - 5. トレーニング資料の配布
                    - output:
"user_setup_complete.yaml"
                - T3_go_live:
                    - prompt: |
                        - 本番稼働：
                        - 1. 最終動作確認
                        - 2. バックアップ設定
                        - 3. 監視アラート設定
                        - 4. ユーザーへの通知
                        - 5. サポート体制の確立
                    - output:
"go_live_checklist.yaml"