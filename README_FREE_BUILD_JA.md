# PCなし・無料のAndroidビルド

## 配布中

[Android free build 7]( https://github.com/akari828-prog/nearby-leisure-finder-demo/releases/tag/android-free-37396900610-1 ) を公開しています。APKはnearby-leisure-free.apk（約48.7 MB）です。

GitHub ActionsでFlutter依存取得、静的解析、イベント分類テスト、Release APKビルド、署名検証が成功しました。実機でのインストールと起動確認はまだです。

## 無料版の内容

- RSSからイベント候補を最大10件取得
- 祭り、マルシェ、展示、観光などを端末内キーワードで分類
- RSSに場所が明記された候補をジオコーディングし、10km以内を近い順で表示
- GPSは検索時だけ取得し、距離計算は端末内で実行
- Firebase、Gemini API、APIキー、支払い方法は不要
- Google公式テスト広告IDを使用

無料版はAIではなくキーワード判定のため、RSSによって見逃しや誤分類があります。開催日時・住所が明記されていない場合は推測で補いません。

## Gemini版の配布停止

Gemini Developer APIの現行追加利用規約に「消費者向けではない」とあるため、Geminiを利用していたAPKを配布から外しました。一般向けの暇つぶしアプリでは利用しない判断です。公式規約: https://ai.google.dev/gemini-api/terms

## ビルド費用

このアプリではFirebase、Gemini API、Cloud Billingを使いません。GitHub Actionsは公開リポジトリの標準ランナーを利用します。GitHub公式説明では公開リポジトリの標準GitHub-hosted runnerは無料です: https://docs.github.com/en/actions/reference/runners/github-hosted-runners

## ソースの設定場所

- RSSと地域検索語: lib/config/app_config.dart
- 端末内の分類語: lib/services/local_event_classifier.dart
- Google公式テスト広告ユニットID: lib/config/ad_config.dart
- テスト用AdMob App ID: android/app/build.gradle.kts

ソースZIPとワークフローはGitHubリポジトリにあります。ビルドの詳細は[スマートフォン向け手順](README_PHONE_JA.md)を参照してください。
