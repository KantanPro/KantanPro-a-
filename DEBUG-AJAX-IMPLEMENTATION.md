## AJAX エラー解決のためのデバッグ改善

### 実装したデバッグ機能

1. **JavaScript デバッグスクリプト (`debug-ajax.js`)**
   - AJAX リクエストの詳細ログ
   - 400エラーの分析
   - リクエスト/レスポンスデータの解析
   - 手動デバッグ出力 (Ctrl+Shift+D)

2. **PHP デバッグハンドラー (`debug-ajax-handler.php`)**
   - サーバーサイドのAJAXリクエスト監視
   - PHP エラーの詳細ログ
   - HTTPレスポンスステータスの監視
   - ログファイルへの記録

3. **統合デバッグ機能**
   - デバッグモード時のみ動作
   - フロントエンド・バックエンド両方のログ
   - 管理者向けログ表示機能

### 使用方法

1. **WordPress で `WP_DEBUG` を有効にする**
   ```php
   define( 'WP_DEBUG', true );
   define( 'WP_DEBUG_LOG', true );
   ```

2. **ブラウザでデバッグ情報を確認**
   - `Ctrl+Shift+D` でデバッグ情報を表示
   - コンソールでAJAXエラーの詳細を確認

3. **サーバーログを確認**
   ```javascript
   // ブラウザコンソールで実行
   KTPAjaxDebug.showServerLog(100);  // 最新100行を表示
   KTPAjaxDebug.clearServerLog();    // ログをクリア
   ```

### 次のステップ

1. **デバッグモードを有効にして実際のエラーを確認**
2. **400エラーの具体的な原因を特定**
3. **必要に応じて該当のAJAXハンドラーを修正**

### 既知の問題と解決策

- **nonce 検証失敗**: nonceの生成と検証を適切に実装
- **missing action**: AJAXリクエストにactionパラメータを確実に含める
- **権限エラー**: 適切なユーザー権限チェックを実装
- **PHP エラー**: サーバーエラーログで詳細を確認

このデバッグシステムにより、400エラーの根本原因を特定し、適切な修正を実施できます。
