# C9: テスト・検証

システムの動作確認と検証を実施し、品質を保証します。

## テストフェーズ概要

```
単体テスト (Unit Testing)
    ├── 統合テスト (Integration Testing)
    │   ├── パフォーマンステスト (Performance Testing)
    │   │   └── 受入テスト (UAT)
```

## タスク実行手順

### T1: 単体テスト

各機能の個別動作確認：

```yaml
unit_test_checklist:
  field_calculations:
    - test_name: "数式フィールド計算精度"
      test_cases:
        - case: "基本計算"
          input: "売上: 1000, 税率: 10%"
          expected: "税額: 100, 合計: 1100"
          status: "[ ] Pass / [ ] Fail"
        
        - case: "ゼロ除算処理"
          input: "分子: 100, 分母: 0"
          expected: "エラーメッセージ表示"
          status: "[ ] Pass / [ ] Fail"
        
        - case: "NULL値処理"
          input: "売上: NULL, 税率: 10%"
          expected: "税額: 0 または空白"
          status: "[ ] Pass / [ ] Fail"
        
        - case: "境界値テスト"
          input: "最大値、最小値、負の値"
          expected: "適切な処理と表示"
          status: "[ ] Pass / [ ] Fail"
  
  link_integrity:
    - test_name: "リレーション参照整合性"
      test_cases:
        - case: "親レコード削除時"
          action: "親レコードを削除"
          expected: "子レコードの参照がNULLまたはエラー"
          status: "[ ] Pass / [ ] Fail"
        
        - case: "循環参照チェック"
          action: "A→B→C→Aの参照を作成"
          expected: "エラーまたは警告表示"
          status: "[ ] Pass / [ ] Fail"
        
        - case: "多対多リレーション"
          action: "複数レコード間のリンク"
          expected: "双方向で正しく表示"
          status: "[ ] Pass / [ ] Fail"
  
  workflow_execution:
    - test_name: "ワークフロー動作確認"
      test_cases:
        - case: "トリガー発火"
          condition: "ステータス = '承認申請'"
          expected: "ワークフローが起動"
          status: "[ ] Pass / [ ] Fail"
        
        - case: "条件分岐"
          condition: "金額 > 100万円"
          expected: "上位承認者へエスカレーション"
          status: "[ ] Pass / [ ] Fail"
        
        - case: "エラーハンドリング"
          condition: "承認者不在"
          expected: "代理承認者へ自動転送"
          status: "[ ] Pass / [ ] Fail"
  
  button_actions:
    - test_name: "ボタンアクション実行"
      test_cases:
        - case: "レコード作成ボタン"
          action: "クリック"
          expected: "新規レコード作成と初期値設定"
          status: "[ ] Pass / [ ] Fail"
        
        - case: "一括更新ボタン"
          action: "10件選択して実行"
          expected: "全件正常更新"
          status: "[ ] Pass / [ ] Fail"
        
        - case: "外部連携ボタン"
          action: "API呼び出し"
          expected: "正常レスポンスとデータ反映"
          status: "[ ] Pass / [ ] Fail"
  
  permission_control:
    - test_name: "権限制御動作"
      test_cases:
        - case: "閲覧権限のみ"
          user: "viewer_role"
          action: "編集を試行"
          expected: "編集不可メッセージ"
          status: "[ ] Pass / [ ] Fail"
        
        - case: "フィールドレベル権限"
          user: "editor_role"
          action: "機密フィールド表示"
          expected: "マスキングまたは非表示"
          status: "[ ] Pass / [ ] Fail"
```

### T2: 統合テスト

エンドツーエンドの業務フロー確認：

```json
{
  "integration_test_scenarios": [
    {
      "scenario_name": "受注から出荷までの一連フロー",
      "steps": [
        {
          "step": 1,
          "action": "新規注文レコード作成",
          "data": {
            "顧客": "テスト商事",
            "商品": "テスト商品A",
            "数量": 10
          },
          "expected": "注文番号自動採番、在庫引当",
          "result": ""
        },
        {
          "step": 2,
          "action": "承認申請ワークフロー起動",
          "trigger": "ステータス変更",
          "expected": "承認者へ通知送信",
          "result": ""
        },
        {
          "step": 3,
          "action": "承認処理",
          "user": "manager_user",
          "expected": "ステータス更新、次工程開始",
          "result": ""
        },
        {
          "step": 4,
          "action": "出荷処理",
          "data": {
            "出荷日": "TODAY()",
            "配送業者": "テスト運送"
          },
          "expected": "在庫減少、売上計上",
          "result": ""
        },
        {
          "step": 5,
          "action": "完了確認",
          "checks": [
            "在庫数が正しく減少",
            "売上レコードが作成",
            "ダッシュボードに反映",
            "履歴ログが記録"
          ],
          "result": ""
        }
      ],
      "overall_result": "[ ] Pass / [ ] Fail"
    },
    {
      "scenario_name": "月次締め処理",
      "steps": [
        {
          "step": 1,
          "action": "締め処理ボタン実行",
          "expected": "当月データの集計開始",
          "result": ""
        },
        {
          "step": 2,
          "action": "自動計算処理",
          "checks": [
            "売上集計の正確性",
            "在庫評価の計算",
            "未処理データの検出"
          ],
          "result": ""
        },
        {
          "step": 3,
          "action": "レポート生成",
          "expected": "月次レポート自動作成",
          "result": ""
        }
      ],
      "overall_result": "[ ] Pass / [ ] Fail"
    }
  ]
}
```

### T3: パフォーマンステスト

負荷とレスポンスタイムの確認：

```yaml
performance_test_results:
  data_volume_test:
    test_name: "大量データ処理"
    test_conditions:
      - record_count: 1000
        response_time: "0.5秒"
        result: "Pass"
      
      - record_count: 10000
        response_time: "1.2秒"
        result: "Pass"
      
      - record_count: 50000
        response_time: "3.5秒"
        result: "Pass"
      
      - record_count: 100000
        response_time: "8.2秒"
        result: "Warning - 要最適化"
    
    target_performance:
      acceptable: "5秒以内"
      optimal: "2秒以内"
  
  formula_calculation_test:
    test_name: "複雑な数式計算速度"
    test_cases:
      - formula_complexity: "単純計算（加減乗除）"
        fields_count: 10
        response_time: "即時"
        result: "Pass"
      
      - formula_complexity: "条件分岐含む"
        fields_count: 20
        response_time: "0.1秒"
        result: "Pass"
      
      - formula_complexity: "ルックアップ+集計"
        fields_count: 50
        response_time: "0.8秒"
        result: "Pass"
      
      - formula_complexity: "ネスト関数多用"
        fields_count: 100
        response_time: "2.5秒"
        result: "Warning"
  
  workflow_processing_test:
    test_name: "ワークフロー処理速度"
    test_cases:
      - workflow_type: "単純更新"
        trigger_count: 10
        processing_time: "1秒"
        result: "Pass"
      
      - workflow_type: "承認フロー"
        trigger_count: 50
        processing_time: "5秒"
        result: "Pass"
      
      - workflow_type: "連鎖処理"
        trigger_count: 100
        processing_time: "15秒"
        result: "Warning"
  
  concurrent_access_test:
    test_name: "同時アクセス安定性"
    test_cases:
      - concurrent_users: 10
        operations: "読み取り中心"
        stability: "安定"
        errors: 0
      
      - concurrent_users: 50
        operations: "読み書き混在"
        stability: "安定"
        errors: 0
      
      - concurrent_users: 100
        operations: "大量更新"
        stability: "やや遅延"
        errors: 2
      
      - concurrent_users: 200
        operations: "ピーク時想定"
        stability: "要対策"
        errors: 5
```

## 出力例

### unit_test_results.yaml
```yaml
unit_test_summary:
  test_date: "2024-01-20"
  total_tests: 45
  passed: 42
  failed: 2
  skipped: 1
  
  test_categories:
    field_calculations:
      total: 12
      passed: 11
      failed: 1
      issues:
        - test: "極大値処理"
          issue: "オーバーフロー発生"
          severity: "Medium"
          fix_status: "対応中"
    
    link_integrity:
      total: 8
      passed: 8
      failed: 0
      notes: "全テスト合格"
    
    workflow_execution:
      total: 10
      passed: 9
      failed: 1
      issues:
        - test: "タイムアウト処理"
          issue: "30秒で強制終了せず"
          severity: "Low"
          fix_status: "次回リリース"
    
    button_actions:
      total: 8
      passed: 8
      failed: 0
      notes: "全テスト合格"
    
    permission_control:
      total: 7
      passed: 6
      failed: 0
      skipped: 1
      notes: "LDAP連携テストは環境構築後"
```

### integration_test_results.yaml
```yaml
integration_test_report:
  test_period: "2024-01-15 to 2024-01-20"
  scenarios_tested: 8
  scenarios_passed: 7
  scenarios_failed: 1
  
  detailed_results:
    - scenario: "受注から出荷フロー"
      status: "Pass"
      duration: "15分"
      notes: "全工程正常動作確認"
    
    - scenario: "月次締め処理"
      status: "Pass"
      duration: "8分"
      notes: "集計値の精度確認済"
    
    - scenario: "在庫補充フロー"
      status: "Pass"
      duration: "12分"
      notes: "アラート発火確認"
    
    - scenario: "返品処理フロー"
      status: "Fail"
      duration: "10分"
      failure_point: "在庫戻し処理"
      issue: "ステータス更新タイミング"
      fix_eta: "2024-01-22"
  
  data_integrity_check:
    tables_checked: 15
    integrity_issues: 0
    orphan_records: 0
    duplicate_checks: "Pass"
```

### performance_test_results.yaml
```yaml
performance_test_summary:
  test_environment:
    date: "2024-01-20"
    data_volume: "10万レコード"
    concurrent_users: "100"
    test_duration: "2時間"
  
  results:
    response_times:
      average: "1.2秒"
      median: "0.8秒"
      95_percentile: "2.5秒"
      99_percentile: "4.8秒"
      max: "8.2秒"
    
    throughput:
      requests_per_second: 450
      successful_requests: 99.8%
      error_rate: 0.2%
    
    resource_usage:
      cpu_average: 65%
      cpu_peak: 85%
      memory_average: 4.2GB
      memory_peak: 6.8GB
    
    bottlenecks_identified:
      - component: "複雑な集計ビュー"
        impact: "High"
        recommendation: "インデックス追加"
      
      - component: "大量データエクスポート"
        impact: "Medium"
        recommendation: "非同期処理化"
    
  optimization_recommendations:
    immediate:
      - "頻繁にアクセスされるビューのキャッシュ"
      - "重い計算フィールドの事前計算"
    
    short_term:
      - "データベースインデックスの最適化"
      - "ワークフローの並列処理"
    
    long_term:
      - "アーカイブ戦略の実装"
      - "読み取り専用レプリカの検討"
```

## テスト自動化スクリプト

```bash
#!/bin/bash
# test_automation.sh

echo "=== Lark Base System Test Suite ==="
echo "Starting at: $(date)"

# 単体テスト実行
echo -e "\n[1/3] Running Unit Tests..."
# フィールド計算テスト
# リンク整合性テスト
# 権限テスト

# 統合テスト実行
echo -e "\n[2/3] Running Integration Tests..."
# シナリオベーステスト
# データフローテスト

# パフォーマンステスト実行
echo -e "\n[3/3] Running Performance Tests..."
# 負荷テスト
# 同時実行テスト

echo -e "\nTest completed at: $(date)"
echo "Generating test report..."
```

## テストのベストプラクティス

1. **テスト環境の分離**
   - 本番データのコピーを使用
   - テスト後のクリーンアップ
   - 環境間の差異を最小化

2. **継続的テスト**
   - 日次での自動テスト実行
   - 変更時の回帰テスト
   - パフォーマンス監視

3. **テストデータ管理**
   - 現実的なテストデータ
   - エッジケースの網羅
   - 個人情報のマスキング

4. **結果の可視化**
   - ダッシュボードでの表示
   - 傾向分析とレポート
   - 問題の早期発見

実施後は、テスト結果を分析し、発見された問題の優先順位付けと対応を行ってください。