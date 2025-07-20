# C8: 権限設定

階層的な権限を設定し、セキュアなアクセス制御を実現します。

## 権限階層構造

```
管理者 (Admin)
    ├── マネージャー (Manager)
    │   ├── 編集者 (Editor)
    │   │   ├── 投稿者 (Contributor)
    │   │   │   └── 閲覧者 (Viewer)
```

## タスク実行手順

### T1: 権限ロール定義

5段階の権限ロールを定義：

```yaml
role_definitions:
  admin:
    name: "管理者（Admin）"
    description: "システム全体の管理権限"
    permissions:
      - "全機能へのフルアクセス"
      - "システム設定変更"
      - "権限管理"
      - "データ削除"
      - "監査ログ閲覧"
      - "バックアップ・リストア"
    restrictions: []
    
  manager:
    name: "マネージャー（Manager）"
    description: "部門管理とレポート作成権限"
    permissions:
      - "承認権限"
      - "レポート作成"
      - "部門間データ閲覧"
      - "一部設定変更"
      - "ダッシュボード編集"
      - "ワークフロー作成"
    restrictions:
      - "システム設定変更不可"
      - "権限管理不可"
      
  editor:
    name: "編集者（Editor）"
    description: "データ作成・編集権限"
    permissions:
      - "データ作成・編集"
      - "自部門データ管理"
      - "ワークフロー実行"
      - "エクスポート"
      - "ビュー作成"
      - "フィルター保存"
    restrictions:
      - "他部門データ編集不可"
      - "削除は自データのみ"
      
  contributor:
    name: "投稿者（Contributor）"
    description: "限定的なデータ作成権限"
    permissions:
      - "データ作成"
      - "自分のデータ編集"
      - "コメント追加"
      - "基本的な閲覧"
      - "個人ビュー作成"
    restrictions:
      - "他者データ編集不可"
      - "一括操作不可"
      
  viewer:
    name: "閲覧者（Viewer）"
    description: "閲覧専用権限"
    permissions:
      - "データ閲覧のみ"
      - "コメント閲覧"
      - "公開レポート閲覧"
    restrictions:
      - "ダウンロード不可"
      - "編集不可"
      - "コメント投稿不可"
```

### T2: テーブル権限マトリックス

テーブル別の権限設定：

```json
{
  "table_permissions": {
    "マスターデータ": {
      "admin": {
        "create": true,
        "read": true,
        "update": true,
        "delete": true,
        "export": true,
        "import": true
      },
      "manager": {
        "create": false,
        "read": true,
        "update": true,
        "delete": false,
        "export": true,
        "import": false
      },
      "editor": {
        "create": false,
        "read": true,
        "update": {
          "allowed": true,
          "excluded_fields": ["原価", "利益率", "承認者"]
        },
        "delete": false,
        "export": true,
        "import": false
      },
      "contributor": {
        "create": false,
        "read": true,
        "update": false,
        "delete": false,
        "export": false,
        "import": false
      },
      "viewer": {
        "create": false,
        "read": {
          "allowed": true,
          "excluded_fields": ["原価", "利益率", "個人情報"]
        },
        "update": false,
        "delete": false,
        "export": false,
        "import": false
      }
    },
    "トランザクションデータ": {
      "admin": {
        "create": true,
        "read": true,
        "update": true,
        "delete": true,
        "export": true,
        "approve": true
      },
      "manager": {
        "create": true,
        "read": true,
        "update": true,
        "delete": false,
        "export": true,
        "approve": true
      },
      "editor": {
        "create": true,
        "read": {
          "scope": "own_department"
        },
        "update": {
          "scope": "own_data"
        },
        "delete": {
          "scope": "own_data",
          "time_limit": "24hours"
        },
        "export": true,
        "approve": false
      },
      "contributor": {
        "create": true,
        "read": {
          "scope": "own_data"
        },
        "update": {
          "scope": "own_data",
          "status_restriction": ["draft", "new"]
        },
        "delete": false,
        "export": false,
        "approve": false
      },
      "viewer": {
        "create": false,
        "read": {
          "scope": "public_data"
        },
        "update": false,
        "delete": false,
        "export": false,
        "approve": false
      }
    }
  }
}
```

### T3: フィールドレベル権限

機密フィールドの詳細な権限設定：

```json
{
  "field_permissions": {
    "財務情報": {
      "原価": {
        "display": ["admin", "manager", "finance_editor"],
        "edit": ["admin", "finance_editor"],
        "formula_access": ["admin"],
        "export": ["admin", "manager"]
      },
      "利益率": {
        "display": ["admin", "manager", "sales_manager"],
        "edit": ["admin"],
        "formula_access": ["admin", "manager"],
        "export": ["admin", "manager"]
      },
      "予算": {
        "display": ["admin", "manager", "department_head"],
        "edit": ["admin", "finance_manager"],
        "formula_access": ["admin", "manager"],
        "export": ["admin"]
      }
    },
    "個人情報": {
      "給与": {
        "display": ["admin", "hr_manager", "self"],
        "edit": ["admin", "hr_manager"],
        "formula_access": ["admin"],
        "export": ["admin"]
      },
      "評価": {
        "display": ["admin", "direct_manager", "hr_manager", "self"],
        "edit": ["admin", "direct_manager", "hr_manager"],
        "formula_access": ["admin", "hr_manager"],
        "export": ["admin", "hr_manager"]
      },
      "個人連絡先": {
        "display": ["admin", "hr_team", "direct_manager", "self"],
        "edit": ["admin", "hr_team", "self"],
        "formula_access": [],
        "export": ["admin"]
      }
    },
    "機密情報": {
      "APIキー": {
        "display": ["admin", "system_admin"],
        "edit": ["admin"],
        "formula_access": [],
        "export": []
      },
      "パスワード": {
        "display": [],
        "edit": ["self"],
        "formula_access": [],
        "export": []
      }
    }
  }
}
```

## 出力例

### role_definition.yaml
```yaml
roles:
  - id: "admin"
    name: "管理者"
    level: 1
    parent: null
    capabilities:
      system:
        - manage_users
        - manage_roles
        - manage_settings
        - view_audit_logs
        - manage_backup
      data:
        - full_access
        - bulk_operations
        - import_export
        - delete_permanent
      workflow:
        - create_workflow
        - edit_all_workflows
        - delete_workflow
        - override_approval
      reporting:
        - create_dashboard
        - edit_all_dashboards
        - access_all_reports
        - schedule_reports
        
  - id: "manager"
    name: "マネージャー"
    level: 2
    parent: "admin"
    capabilities:
      system:
        - view_department_logs
        - manage_department_users
      data:
        - read_all_department
        - update_all_department
        - approve_changes
        - export_data
      workflow:
        - create_workflow
        - edit_own_workflows
        - execute_all_workflows
      reporting:
        - create_dashboard
        - edit_own_dashboards
        - access_department_reports
        - schedule_reports
```

### table_permissions.json
```json
{
  "permission_matrix": {
    "tables": [
      {
        "table_name": "顧客マスタ",
        "permissions": {
          "admin": "CRUD",
          "manager": "RU",
          "editor": "RU*",
          "contributor": "R",
          "viewer": "R*"
        },
        "notes": {
          "editor": "機密フィールド除く",
          "viewer": "公開フィールドのみ"
        }
      },
      {
        "table_name": "注文データ",
        "permissions": {
          "admin": "CRUD+A",
          "manager": "CRU+A",
          "editor": "CRU",
          "contributor": "CR",
          "viewer": "R"
        },
        "scope": {
          "editor": "自部門データ",
          "contributor": "自己作成データ",
          "viewer": "公開済みデータ"
        }
      }
    ],
    "legend": {
      "C": "Create",
      "R": "Read",
      "U": "Update",
      "D": "Delete",
      "A": "Approve",
      "*": "制限付き"
    }
  }
}
```

### field_permissions.json
```json
{
  "sensitive_fields": [
    {
      "field_name": "原価",
      "table": "商品マスタ",
      "classification": "confidential",
      "permissions": {
        "view": {
          "roles": ["admin", "manager", "purchasing_team"],
          "condition": null
        },
        "edit": {
          "roles": ["admin", "purchasing_manager"],
          "condition": "status != 'approved'"
        },
        "export": {
          "roles": ["admin"],
          "requires_approval": true
        }
      },
      "masking": {
        "enabled": true,
        "type": "partial",
        "format": "****"
      }
    },
    {
      "field_name": "個人情報",
      "table": "従業員マスタ",
      "classification": "pii",
      "permissions": {
        "view": {
          "roles": ["admin", "hr_team"],
          "condition": "department = user.department OR record.id = user.id"
        },
        "edit": {
          "roles": ["admin", "hr_manager"],
          "condition": "record.id = user.id AND field IN ['連絡先', '緊急連絡先']"
        },
        "export": {
          "roles": [],
          "requires_approval": false
        }
      },
      "encryption": {
        "at_rest": true,
        "in_transit": true
      }
    }
  ]
}
```

## 権限設定のベストプラクティス

### 1. 最小権限の原則
```yaml
principle_of_least_privilege:
  - デフォルトは最小権限から開始
  - 必要に応じて権限を追加
  - 定期的な権限レビュー実施
  - 不要な権限の即座の削除
```

### 2. 職務分離
```yaml
segregation_of_duties:
  - 作成者と承認者の分離
  - データ入力と検証の分離
  - 設定変更と監査の分離
```

### 3. 監査とコンプライアンス
```yaml
audit_compliance:
  - 全権限変更の記録
  - アクセスログの保持
  - 定期的な権限監査
  - コンプライアンス要件の確認
```

### 4. 例外処理
```yaml
exception_handling:
  - 臨時権限の期限設定
  - 承認プロセスの明確化
  - 緊急時アクセスの手順
  - 事後レビューの実施
```

## 実装チェックリスト

- [ ] 全ロールの定義完了
- [ ] テーブル権限マトリックスの設定
- [ ] 機密フィールドの特定と保護
- [ ] 承認フローとの整合性確認
- [ ] 監査ログの有効化
- [ ] 権限テストの実施
- [ ] ドキュメントの作成
- [ ] ユーザートレーニングの実施

実装後は定期的に権限設定をレビューし、組織の変更に応じて更新してください。