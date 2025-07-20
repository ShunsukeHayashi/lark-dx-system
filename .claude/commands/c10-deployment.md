# C10: デプロイ・移行

本番環境への展開と既存システムからの移行を実施します。

## デプロイメントフェーズ

```
準備フェーズ
    ├── データ移行フェーズ
    │   ├── ユーザー設定フェーズ
    │   │   └── 本番稼働フェーズ
```

## タスク実行手順

### T1: データ移行

既存データの移行プロセス：

```yaml
data_migration_plan:
  phase1_preparation:
    data_analysis:
      - task: "既存データ構造の分析"
        actions:
          - "テーブル構成の確認"
          - "データ型のマッピング"
          - "文字コードの確認"
          - "NULL値の扱い確認"
        output: "data_mapping.xlsx"
      
      - task: "データクレンジング"
        actions:
          - "重複データの特定と処理"
          - "不正データの修正"
          - "欠損値の補完"
          - "形式の統一"
        tools:
          - "Excel/Google Sheets"
          - "Python pandas"
          - "データ検証スクリプト"
    
    master_data_preparation:
      - task: "マスターデータ整理"
        priority: "最優先"
        data_sets:
          - name: "顧客マスタ"
            records: 5000
            fields_mapping:
              old_system: ["customer_id", "name", "tel", "address"]
              lark_base: ["顧客ID", "顧客名", "電話番号", "住所"]
          
          - name: "商品マスタ"
            records: 2000
            fields_mapping:
              old_system: ["item_code", "item_name", "price", "stock"]
              lark_base: ["商品コード", "商品名", "単価", "在庫数"]
          
          - name: "従業員マスタ"
            records: 200
            fields_mapping:
              old_system: ["emp_id", "emp_name", "dept", "email"]
              lark_base: ["従業員ID", "従業員名", "部署", "メール"]
    
  phase2_migration:
    import_sequence:
      - step: 1
        table: "部署マスタ"
        method: "CSV import"
        validation: "部署コードのユニーク性確認"
        rollback: "DELETE FROM 部署マスタ WHERE import_batch = '{{batch_id}}'"
      
      - step: 2
        table: "従業員マスタ"
        method: "CSV import"
        validation: "部署との参照整合性確認"
        dependency: "部署マスタ"
      
      - step: 3
        table: "顧客マスタ"
        method: "API batch insert"
        validation: "顧客IDの重複チェック"
        batch_size: 1000
      
      - step: 4
        table: "商品マスタ"
        method: "CSV import"
        validation: "商品コードのユニーク性、価格の妥当性"
      
      - step: 5
        table: "取引データ"
        method: "分割インポート"
        validation: "顧客・商品の参照確認、金額計算の検証"
        batch_size: 5000
        parallel: true
    
    validation_checks:
      - check: "レコード数の一致"
        query: "SELECT COUNT(*) FROM each_table"
        tolerance: 0
      
      - check: "金額合計の一致"
        query: "SELECT SUM(amount) FROM transactions"
        tolerance: 0.01
      
      - check: "参照整合性"
        query: "Foreign key validation queries"
        tolerance: 0
      
      - check: "必須フィールドの充足"
        query: "NULL check queries"
        tolerance: 0
```

### T2: ユーザー設定

ユーザーアカウントと権限の設定：

```json
{
  "user_setup_process": {
    "account_creation": {
      "method": "bulk_import",
      "source": "existing_user_list.csv",
      "fields": [
        "email",
        "name",
        "department",
        "role",
        "manager_email"
      ],
      "authentication": {
        "method": "SSO",
        "provider": "corporate_idp",
        "fallback": "email_invitation"
      }
    },
    
    "role_assignment": {
      "mapping_rules": [
        {
          "condition": "title CONTAINS 'Manager' OR grade >= 'M1'",
          "assign_role": "manager"
        },
        {
          "condition": "department IN ('Sales', 'Marketing', 'Operations')",
          "assign_role": "editor"
        },
        {
          "condition": "employment_type = 'contractor'",
          "assign_role": "contributor"
        },
        {
          "condition": "department = 'Audit' OR title CONTAINS 'Auditor'",
          "assign_role": "viewer"
        }
      ],
      "default_role": "contributor"
    },
    
    "initial_settings": {
      "notification_preferences": {
        "email": true,
        "in_app": true,
        "mobile_push": false,
        "frequency": "immediate"
      },
      "language": "ja",
      "timezone": "Asia/Tokyo",
      "date_format": "YYYY-MM-DD",
      "week_start": "monday"
    },
    
    "training_assignment": {
      "mandatory_courses": [
        {
          "course": "Lark Base基礎",
          "duration": "30分",
          "deadline": "login + 7 days"
        },
        {
          "course": "セキュリティガイドライン",
          "duration": "15分",
          "deadline": "login + 3 days"
        }
      ],
      "role_specific_training": {
        "admin": ["管理者機能", "権限管理", "監査ログ"],
        "manager": ["承認フロー", "レポート作成", "ダッシュボード"],
        "editor": ["データ入力", "ワークフロー", "ビュー操作"]
      }
    }
  }
}
```

### T3: 本番稼働

最終確認と本番環境への切り替え：

```yaml
go_live_checklist:
  final_verification:
    system_checks:
      - item: "全機能の動作確認"
        responsible: "システム管理者"
        status: "[ ] 完了"
        notes: "単体・統合テスト結果を参照"
      
      - item: "データ移行の完全性確認"
        responsible: "データ管理者"
        status: "[ ] 完了"
        validation:
          - "レコード数の一致"
          - "金額の照合"
          - "マスターデータの整合性"
      
      - item: "権限設定の確認"
        responsible: "セキュリティ管理者"
        status: "[ ] 完了"
        checks:
          - "各ロールのアクセステスト"
          - "機密データの保護確認"
      
      - item: "パフォーマンステスト合格"
        responsible: "インフラ管理者"
        status: "[ ] 完了"
        criteria: "レスポンスタイム < 3秒"
    
    backup_setup:
      - type: "自動バックアップ"
        frequency: "日次"
        time: "02:00 JST"
        retention: "30日間"
        storage: "クラウドストレージ"
      
      - type: "スナップショット"
        frequency: "週次"
        day: "日曜日"
        retention: "3ヶ月"
      
      - type: "アーカイブ"
        frequency: "月次"
        retention: "1年"
        compression: true
    
    monitoring_alerts:
      - alert: "システムダウン検知"
        condition: "availability < 99%"
        notification: ["admin@company.com", "oncall@company.com"]
        escalation: "15分後に上位管理者へ"
      
      - alert: "パフォーマンス劣化"
        condition: "response_time > 5秒 for 5分"
        notification: ["sysadmin@company.com"]
      
      - alert: "エラー率上昇"
        condition: "error_rate > 1%"
        notification: ["dev-team@company.com"]
      
      - alert: "ストレージ容量"
        condition: "usage > 80%"
        notification: ["infra@company.com"]
    
    communication_plan:
      - audience: "全社員"
        message: "新システム稼働開始のお知らせ"
        channel: "email"
        timing: "稼働日の1週間前"
      
      - audience: "キーユーザー"
        message: "切り替え手順の詳細"
        channel: "Teams/Slack"
        timing: "稼働日の3日前"
      
      - audience: "管理者"
        message: "緊急時対応手順"
        channel: "直接連絡"
        timing: "稼働日前日"
    
    support_structure:
      tier1:
        name: "ヘルプデスク"
        hours: "平日 9:00-18:00"
        contact: "helpdesk@company.com"
        scope: "基本的な操作サポート"
      
      tier2:
        name: "システム管理者"
        hours: "平日 8:00-20:00"
        contact: "sysadmin@company.com"
        scope: "技術的な問題対応"
      
      tier3:
        name: "開発チーム"
        hours: "オンコール"
        contact: "dev-oncall@company.com"
        scope: "緊急障害対応"
```

## 出力例

### migration_log.yaml
```yaml
migration_summary:
  start_time: "2024-01-20 20:00:00"
  end_time: "2024-01-21 02:30:00"
  total_duration: "6時間30分"
  status: "成功"
  
  tables_migrated:
    - table: "部署マスタ"
      records: 50
      status: "完了"
      duration: "1分"
      errors: 0
    
    - table: "従業員マスタ"
      records: 200
      status: "完了"
      duration: "3分"
      errors: 0
    
    - table: "顧客マスタ"
      records: 5000
      status: "完了"
      duration: "15分"
      errors: 2
      error_details:
        - "重複キー: CUS001 (スキップ)"
        - "不正な郵便番号: CUS2345 (修正済)"
    
    - table: "商品マスタ"
      records: 2000
      status: "完了"
      duration: "8分"
      errors: 0
    
    - table: "取引データ"
      records: 150000
      status: "完了"
      duration: "2時間"
      errors: 15
      error_handling: "エラーログ出力、手動修正予定"
  
  validation_results:
    record_count_check: "Pass"
    amount_reconciliation: "Pass (差異: 0.00)"
    referential_integrity: "Pass"
    required_fields: "Pass"
  
  post_migration_tasks:
    - "エラーレコードの手動修正"
    - "インデックスの再構築"
    - "統計情報の更新"
```

### user_setup_complete.yaml
```yaml
user_provisioning_report:
  date: "2024-01-22"
  total_users: 200
  successfully_created: 198
  failed: 2
  
  role_distribution:
    admin: 5
    manager: 25
    editor: 100
    contributor: 50
    viewer: 18
  
  department_distribution:
    sales: 45
    operations: 60
    finance: 20
    hr: 15
    it: 10
    management: 25
    others: 23
  
  authentication_status:
    sso_enabled: 180
    email_invitation_sent: 18
    pending_activation: 2
  
  training_assignment:
    assigned: 198
    completed: 150
    in_progress: 40
    not_started: 8
  
  issues_encountered:
    - user: "john.doe@company.com"
      issue: "メールアドレス不正"
      resolution: "修正後、再送信"
    
    - user: "jane.smith@company.com"
      issue: "部署コード不明"
      resolution: "デフォルト部署に割り当て"
```

### go_live_checklist.yaml
```yaml
go_live_status:
  scheduled_date: "2024-01-25 00:00"
  current_status: "準備完了"
  
  checklist_completion:
    system_verification: "100%"
    data_migration: "100%"
    user_setup: "99%"
    backup_configuration: "100%"
    monitoring_setup: "100%"
    communication: "100%"
    support_readiness: "100%"
  
  final_approvals:
    - approver: "CTO"
      status: "承認済"
      date: "2024-01-24 15:00"
    
    - approver: "事業部長"
      status: "承認済"
      date: "2024-01-24 16:00"
    
    - approver: "セキュリティ責任者"
      status: "承認済"
      date: "2024-01-24 16:30"
  
  rollback_plan:
    trigger_conditions:
      - "重大なデータ損失"
      - "システム全体のダウン"
      - "セキュリティ侵害"
    
    procedure:
      - "新システムへのアクセス停止"
      - "最新バックアップからの復元"
      - "旧システムへの切り戻し"
      - "影響調査と対策"
    
    estimated_time: "2時間"
    responsible_team: "インフラチーム"
  
  post_launch_monitoring:
    day1:
      - "システム稼働状況の監視"
      - "ユーザーアクセスログの確認"
      - "エラー率のモニタリング"
      - "パフォーマンス指標の追跡"
    
    week1:
      - "ユーザーフィードバックの収集"
      - "改善要望の整理"
      - "初期問題の対応"
      - "利用統計の分析"
    
    month1:
      - "定着度の評価"
      - "ROI測定の開始"
      - "最適化計画の策定"
      - "次フェーズの計画"
```

## 移行スクリプトサンプル

```python
# migration_script.py
import pandas as pd
import requests
from datetime import datetime

class LarkBaseMigration:
    def __init__(self, app_token, api_key):
        self.app_token = app_token
        self.api_key = api_key
        self.base_url = "https://open.larksuite.com/open-apis/bitable/v1"
        
    def migrate_table(self, csv_file, table_id, mapping):
        """CSVファイルからLark Baseテーブルへデータ移行"""
        # CSVデータ読み込み
        df = pd.read_csv(csv_file, encoding='utf-8')
        
        # フィールドマッピング適用
        df.rename(columns=mapping, inplace=True)
        
        # バッチ処理
        batch_size = 1000
        total_records = len(df)
        
        for i in range(0, total_records, batch_size):
            batch = df[i:i+batch_size]
            records = batch.to_dict('records')
            
            # API呼び出し
            response = self.create_records(table_id, records)
            
            if response.status_code == 200:
                print(f"Migrated {i+len(batch)}/{total_records} records")
            else:
                print(f"Error at batch {i}: {response.text}")
                
        return True
```

## デプロイメントのベストプラクティス

1. **段階的移行**
   - パイロット部門から開始
   - 段階的な全社展開
   - 各段階でのフィードバック収集

2. **並行稼働期間**
   - 新旧システムの並行運用
   - データ同期の確保
   - 段階的な切り替え

3. **コンティンジェンシープラン**
   - 問題発生時の対応手順
   - ロールバック計画
   - 緊急連絡網の整備

4. **変更管理**
   - ユーザートレーニング
   - ドキュメント整備
   - サポート体制の確立

本番稼働後は、システムの利用状況を継続的にモニタリングし、ユーザーフィードバックに基づいた改善を実施してください。