# 配布先バージョン更新チェック修正完了

## 問題の概要

配布先でバージョン1.1.22(preview)に更新しても、プラグイン一覧で「バージョン 1.1.21(preview)」と表示され続ける問題が発生していました。

## 原因分析

1. **プレビューバージョンの比較ロジック問題**
   - `clean_version`関数でプレビューバージョンを通常版より下位として扱っていた
   - 1.1.22(preview) → 1.1.21.999 として処理され、1.1.21(preview) → 1.1.20.999 より新しいと認識されない

2. **GitHubリリースからの更新情報取得問題**
   - プレビューバージョン間の比較で正しく更新が検出されない
   - 配布先での確実な更新チェック機能が不足

## 実装した修正内容

### 1. プレビューバージョン比較ロジックの修正

**ファイル**: `includes/class-ktpwp-update-checker.php`

```php
// 修正前: プレビューバージョンを下位として扱う
$version_parts[count( $version_parts ) - 1] = max( 0, $last_part - 1 );
$version = implode( '.', $version_parts ) . '.999';

// 修正後: プレビューバージョンを上位として扱う
$version = implode( '.', $version_parts ) . '.1';
```

### 2. 強制更新チェック機能の追加

**プレビューバージョン間の強制比較**:
```php
// 両方ともプレビューバージョンの場合、バージョン番号のみで比較
$latest_version_number = preg_replace( '/\(preview\)/i', '', $data['tag_name'] );
$current_version_number = preg_replace( '/\(preview\)/i', '', $this->current_version );
$force_update = version_compare( $latest_version_number, $current_version_number, '>' );
```

### 3. 初期化時の強制更新チェック

**管理画面初期化時に自動実行**:
```php
// 配布先での確実な更新チェックのため、初期化時に強制更新チェックを実行
if ( is_admin() ) {
    add_action( 'admin_init', array( $this, 'force_update_check_on_init' ), 5 );
}
```

### 4. 更新チェック間隔の緩和

**配布先での確実な更新チェックのため**:
```php
// 配布先での確実な更新チェックのため、間隔制限を緩和
// return false;
```

## 修正効果

### バージョン比較の改善

- **修正前**: 1.1.22(preview) → 1.1.21.999, 1.1.21(preview) → 1.1.20.999
- **修正後**: 1.1.22(preview) → 1.1.22.1, 1.1.21(preview) → 1.1.21.1

### 強制更新チェック

- プレビューバージョン間の比較で、バージョン番号のみを使用
- 1.1.22(preview) > 1.1.21(preview) が正しく認識される

### 自動更新チェック

- 管理画面初期化時に1日1回の強制更新チェックを実行
- 配布先での確実な更新情報取得

## テスト方法

### 1. バージョン比較テスト

```bash
# 現在のバージョン確認
grep "Version:" ktpwp.php

# GitHubリリース確認
curl -s https://api.github.com/repos/KantanPro/freeKTP/releases/latest | grep "tag_name"
```

### 2. 更新チェックテスト

1. 管理画面にログイン
2. プラグイン一覧ページを開く
3. エラーログで更新チェックの実行を確認
4. 更新通知の表示を確認

### 3. 強制更新チェックテスト

```php
// エラーログで以下を確認
// KantanPro: 強制更新チェックを実行しました
// KantanPro: プレビューバージョン強制比較 - 最新: 1.1.22, 現在: 1.1.21, 結果: true
```

## 配布先での動作

### エンドユーザー向け機能

1. **自動更新チェック**: 管理画面アクセス時に自動実行
2. **強制比較**: プレビューバージョン間の確実な比較
3. **更新通知**: 新しいバージョンが利用可能な場合の通知表示

### 手動操作不要

- エンドユーザーが手動でキャッシュクリアする必要なし
- プラグイン更新時に自動的に最新情報を取得
- 管理画面アクセス時に自動的に更新チェックを実行

## 今後の対応

### バージョン管理の改善

1. **プレビューバージョンの命名規則統一**
2. **バージョン比較ロジックの継続的改善**
3. **配布先での更新チェック精度向上**

### 監視とログ

1. **更新チェック実行ログの監視**
2. **バージョン比較結果の記録**
3. **配布先での問題発生時の迅速な対応**

## 完了日時

**2025年1月28日**

この修正により、配布先でバージョン1.1.22(preview)への更新が正しく認識され、プラグイン一覧に最新バージョンが表示されるようになります。 