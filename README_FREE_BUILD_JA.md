# PCなし・無料のAndroidビルド

## 現在の状態

Gemini Developer APIの現行利用規約に合わせ、Geminiを利用していた実検索APKの配布を停止しました。公開中の旧APKはリリースから削除しています。現在、Firebase・Gemini・請求先設定を必要としないRSS＋端末内キーワード判定版をビルドしています。

## 何が必要か

- Androidスマートフォンとブラウザー
- GitHubアカウント（このリポジトリの操作）
- 支払い方法、Firebase登録、APIキーは不要

公開リポジトリのGitHub ActionsがFlutter依存取得、静的解析、テスト、Release APK生成、署名検証を実行します。APKはGitHub Releasesに登録され、スマートフォンからダウンロードできます。

## ビルドの種類

Build free Android APK ワークフローには2種類あります。

- free: RSSから実在候補を取得し、端末内キーワード判定で分類します。
- demo: 東京駅を基準に固定サンプルを表示します。実際に開催されるイベントではありません。

ソースZIP、SHA-256、またはワークフローを更新すると無料版ビルドが自動で開始します。手動実行時は free を選びます。成功した最新APKは [Releases](https://github.com/akari828-prog/nearby-leisure-finder-demo/releases) に **Android free build** として表示されます。

## ソースの設定箇所

- RSSと地域検索語: lib/config/app_config.dart
- 遊びイベントの分類語: lib/services/local_event_classifier.dart
- Google公式テスト広告ユニットID: lib/config/ad_config.dart
- Google公式テストAdMob App ID: android/app/build.gradle.kts

Geminiモデル設定、Firebase AI Logic、App Check、Googleサービス設定ファイルは無料版では使いません。Gemini Developer APIの現行追加利用規約は消費者向けアプリでの利用を認めていないためです。

## 手元でFlutter実行できる場合

~~~sh
flutter pub get
flutter analyze
flutter test
flutter run
flutter build apk
~~~

実検索では位置情報を検索時だけ取得します。Google News RSSの検索には市区町村などのおおまかな地域名が含まれます。GPS座標は端末内の距離計算に使います。
