# 強化版ダミーデータツール

KantanPro WordPressプラグイン用の強化版ダミーデータ作成・クリアツールです。

## 概要

このツールは、KantanProプラグインのテスト用に以下のデータを自動生成します：

- **顧客×6件** - カテゴリー別（テック、不動産、一般、ロジスティック、食品、医療）
- **協力会社×6件** - カテゴリー別（テック、不動産、一般、ロジスティック、食品、教育）
- **サービス×12件** - カテゴリー別・税率自動設定（テック、不動産、一般、ロジスティック、食品、金融）
- **受注書×ランダム件数** - 顧客ごとに2-8件、進捗は重み付きランダム分布
- **職能×18件** - 協力会社×6件 × 税率3パターン（カテゴリー別税率・一般税率・非課税）
- **請求項目とコスト項目** - 各受注書に自動追加

## カテゴリー機能

### 品名ベース税率設定
- **食品関連品名**: 8%（軽減税率）
  - サービス: ケータリングサービス、食材配送、レストラン運営、食品加工、栄養管理、食品安全管理
  - 職能: 食品品質管理、栄養管理、食品安全、食材調達、メニュー開発、衛生管理
- **その他**: 10%（一般税率）
- **不動産関連**: 非課税（非課税取引）

### カテゴリー一覧
1. **テック** - IT・テクノロジー関連（税率10%）
2. **不動産** - 不動産・建設関連（非課税）
3. **一般** - 一般的なサービス（税率10%）
4. **ロジスティック** - 物流・輸送関連（税率10%）
5. **食品** - 食品・飲食関連（税率8%）
6. **医療** - 医療・ヘルスケア関連（税率10%）
7. **教育** - 教育・研修関連（税率10%）
8. **金融** - 金融・保険関連（税率10%）

## 作成されるデータの詳細

### 顧客データ（カテゴリー別）
- **テック**: 株式会社テックソリューション、有限会社デジタルクリエイター、合同会社システム開発、株式会社ウェブデザイン
- **不動産**: 株式会社不動産コンサルティング、有限会社建設工業、合同会社建築設計、株式会社プロパティマネジメント
- **一般**: 株式会社サンプル商事、有限会社コンサルティング、合同会社デザイン工房、株式会社マーケティングプロ
- **ロジスティック**: 株式会社ロジスティクス、有限会社輸送サービス、合同会社倉庫管理、株式会社配送センター
- **食品**: 株式会社フードサービス、有限会社ケータリング、合同会社食材配送、株式会社レストラン運営
- **医療**: 株式会社メディカルサービス、有限会社ヘルスケア、合同会社医療コンサル、株式会社薬局運営

### 協力会社データ（カテゴリー別）
- **テック**: 株式会社テックソリューション、有限会社デジタルクリエイター、合同会社システム開発、株式会社ウェブデザイン
- **不動産**: 株式会社不動産コンサルティング、有限会社建設工業、合同会社建築設計、株式会社プロパティマネジメント
- **一般**: 株式会社サンプル商事、有限会社コンサルティング、合同会社デザイン工房、株式会社マーケティングプロ
- **ロジスティック**: 株式会社ロジスティクス、有限会社輸送サービス、合同会社倉庫管理、株式会社配送センター
- **食品**: 株式会社フードサービス、有限会社ケータリング、合同会社食材配送、株式会社レストラン運営
- **教育**: 株式会社教育サービス、有限会社研修センター、合同会社オンライン教育、株式会社スクール運営

### サービスデータ（品名ベース・税率自動設定）
- **食品関連サービス（税率8%）**
  - ケータリングサービス、食材配送、レストラン運営、食品加工、栄養管理、食品安全管理
- **その他サービス（税率10%）**
  - テック: ウェブサイト制作、システム開発、モバイルアプリ開発、クラウド構築、データベース設計、API開発
  - 不動産: 不動産仲介、物件管理、建築設計、建設工事、不動産投資相談、物件査定
  - 一般: 経営コンサルティング、マーケティング戦略、デザイン制作、翻訳サービス、イベント企画、調査・分析
  - ロジスティック: 物流管理、配送サービス、倉庫管理、輸出入手続き、サプライチェーン管理、配送ルート最適化
  - 金融: 投資コンサルティング、保険相談、会計サービス、税務相談、資産運用、リスク管理

### 受注書データ
- 顧客ごとに2-8件の受注書を作成（ランダム）
- 進捗分布：受付中15%、見積中20%、受注25%、進行中20%、完成15%、請求済5%
- 作成日は過去365日以内のランダムな日付
- 完成済みの受注書には完了日を設定
- 各受注書に請求項目とコスト項目を自動追加

### 職能データ（品名ベース）
- 各協力会社に対して3つの職能を作成
- **食品関連職能がある場合**: 必ず税率8%の職能を1つ含む（税率8%・一般税率10%・一般税率10%）
- **食品関連職能がない場合**: 基本的に一般税率10%（一般税率10%・一般税率10%・非課税）
- **テック**: プログラミング、システム設計、データベース管理、クラウドインフラ、セキュリティ対策、AI・機械学習
- **不動産**: 建築設計、不動産鑑定、施工管理、CAD設計、不動産法務、プロジェクトマネジメント
- **一般**: 経営コンサル、マーケティング、デザイン、翻訳、イベント企画、データ分析
- **ロジスティック**: 物流管理、配送計画、倉庫運営、通関手続き、ルート最適化、在庫管理
- **食品**: 食品品質管理、栄養管理、食品安全、食材調達、メニュー開発、衛生管理
- **医療**: 医療コンサル、看護、薬剤師、医療事務、健康管理、医療機器操作
- **教育**: 講師、教材開発、教育コンサル、オンライン教育、資格指導、カリキュラム設計
- **金融**: 投資コンサル、保険設計、会計、税務、資産運用、リスク管理

## 使用方法

### シェルスクリプトを使用（推奨）

```bash
# ダミーデータを作成
./run-dummy-data.sh create

# ダミーデータをクリア
./run-dummy-data.sh clear

# ヘルプを表示
./run-dummy-data.sh help
```

### PHPスクリプトを直接実行

```bash
# WordPressディレクトリに移動
cd wordpress

# ダミーデータを作成
php ../create_dummy_data.php

# ダミーデータをクリア
php ../create_dummy_data.php clear
```

### WP-CLIを使用

```bash
# WP-CLIコマンドでダミーデータを作成
wp eval-file wp-cli-create-dummy-data.php -- ktp create-dummy-data --force
```

## ファイル構成

- `create_dummy_data.php` - メインのダミーデータ作成スクリプト
- `run-dummy-data.sh` - 実行用シェルスクリプト
- `wp-cli-create-dummy-data.php` - WP-CLI用コマンドファイル

## 機能

### データ作成機能
- 顧客、協力会社、サービス、受注書、職能の一括作成
- カテゴリー別のデータ生成（テック、不動産、一般、ロジスティック、食品、医療、教育、金融）
- カテゴリー別税率の自動設定（食品8%、不動産非課税、その他10%）
- 各受注書に請求項目とコスト項目を自動追加
- リアルな日付と進捗状況の設定
- 重み付きランダム分布による進捗設定

### データクリア機能
- 関連テーブルの一括クリア
- 外部キー制約の適切な処理
- 安全な削除処理

### エラーハンドリング
- テーブル存在チェック
- データベース接続エラーの処理
- 詳細なログ出力

## 注意事項

1. **本番環境での使用禁止** - このツールは開発・テスト環境でのみ使用してください
2. **データバックアップ** - 実行前にデータベースのバックアップを取得してください
3. **WordPress環境** - WordPressが正常に動作している環境で実行してください
4. **権限確認** - データベースへの書き込み権限があることを確認してください

## トラブルシューティング

### よくある問題

1. **WordPressディレクトリが見つからない**
   - スクリプトをKantanProプラグインディレクトリで実行してください

2. **データベース接続エラー**
   - `wp-config.php`の設定を確認してください
   - データベースサーバーが起動していることを確認してください

3. **権限エラー**
   - データベースユーザーに適切な権限があることを確認してください

4. **テーブルが存在しない**
   - KantanProプラグインが正常にインストールされていることを確認してください
   - プラグインのアクティベーションを実行してください

## 更新履歴

- **v2.4.0** - 品名ベース税率設定版
  - 品名に基づく税率設定に変更（食品関連品名は税率8%、その他は10%）
  - 食品関連品名の場合は必ず税率8%を1つ含めるように修正
  - より現実的な税率設定

- **v2.3.1** - 食品カテゴリー税率保証版
  - 食品カテゴリーの協力会社に必ず税率8%の職能を1つ含めるように修正
  - 税率パターンの最適化

- **v2.3.0** - カテゴリー機能追加版
  - カテゴリー機能を追加（テック、不動産、一般、ロジスティック、食品、医療、教育、金融）
  - カテゴリー別税率の自動設定（食品8%、不動産非課税、その他10%）
  - 顧客・サービス・職能にカテゴリーを適用
  - より多様なデータ生成

- **v2.2.8** - 配布先サイト対応版
  - テーブル構造の不一致を修正
  - 受注書作成エラーの解決
  - 配布先サイトでの正常動作を確認

- **v2.0** - 強化版リリース
  - 受注書に請求項目とコスト項目を自動追加
  - データクリア機能を追加
  - 進捗ステータスを3つに絞り込み
  - より詳細なログ出力

- **v1.0** - 初回リリース
  - 基本的なダミーデータ作成機能 