# C1: システム構造分析・設計

## 指示
あなたはLark Baseの専門家です。以下の要件定義とデータ構造設計を行ってください。

## 入力情報
- 業界: $ARGUMENTS
- 業務領域: $ARGUMENTS

## T1: 要件定義
以下の項目を具体的に定義し、`requirement_spec.yaml`として出力してください：

```yaml
application:
  name: "${業界}${業務領域}統合管理システム"
  description: "Lark Baseを活用した統合管理システム"
  
business_requirements:
  main_operations:
    - 主要業務1
    - 主要業務2  
    - 主要業務3
  
scale:
  users: 
    min: 5
    max: 50
  managed_items:
    initial: 1000
    growth: "継続増加見込み"
  partners: 100
  channels: 5
  monthly_transactions:
    min: 1000
    max: 5000
```

## T2: データ構造設計
以下のテーブル構造を設計し、`table_design.yaml`として出力してください：

```yaml
tables:
  master_tables:
    - name: "商品/サービスマスタ"
      type: "static"
      description: "商品・サービスの基本情報管理"
    - name: "取引先マスタ"
      type: "static"
      description: "取引先企業の情報管理"
    - name: "カテゴリマスタ"
      type: "static"
      description: "分類・区分の管理"
      
  transaction_tables:
    - name: "注文/依頼テーブル"
      type: "dynamic"
      description: "受注・依頼の記録"
    - name: "処理/作業テーブル"
      type: "dynamic"
      description: "作業進捗の管理"
    - name: "履歴テーブル"
      type: "dynamic"
      description: "変更履歴の記録"
      
  related_tables:
    - name: "分析用テーブル"
      type: "analytical"
      description: "集計・分析用データ"
    - name: "設定テーブル"
      type: "configuration"
      description: "システム設定値"
```