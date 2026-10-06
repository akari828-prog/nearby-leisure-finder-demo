# PCなし・無料で使うAndroidイベント検索アプリ

## 最新版

実検索版 Android APK（ビルド #6）を公開しました。Firebase AI Logic の Gemini、RSS検索、位置情報検索を含みます。

[APKをダウンロード](https://github.com/akari828-prog/nearby-leisure-finder-demo/releases/tag/android-live-37393697758-1) — Assets の **nearby-leisure-live.apk** を選んでください。

SHA-256: `c34ba49f85f5bdba0b63753e201ccf3de007a61b45c135f0ba3c46b922685724`

## インストール

1. Androidスマートフォンで上のAPKページを開きます。
2. Assetsの **nearby-leisure-live.apk** をダウンロードし、ファイルを開きます。
3. Androidが確認を求めた場合は、APKを開いたブラウザーまたはファイルアプリにインストールを許可します。
4. 「インストール」を押します。位置情報はアプリ内で「現在地から探す」を押した時だけ求められます。

ビルド4のデモAPKは別の署名鍵を使っているため、これをインストールしている場合は削除してからビルド6を入れてください。ビルド5以降は同じ固定署名鍵で更新できます。

## 確認済み

- `flutter pub get` と `flutter analyze` が成功し、解析指摘はありません。
- 実検索版のRelease APKをビルドし、APK署名（v2）を検証しました。登録済みFirebase証明書とSHA-1・SHA-256が一致します。
- Google公式テスト広告IDを使います。
- 実機へのインストールと起動はまだ確認していません。

## 無料設定

FirebaseはSparkプラン（$0）で、Cloud Billingの請求先は登録していません。AIはFirebase AI LogicのGemini Developer API経由で、初期モデルは `gemini-3.5-flash-lite` です。このモデルのテキスト入力・出力には無料枠があります。上限に達した時は検索エラーになり、自動で有料プランへ移行しません。Firebaseの有料プランや支払い情報は設定していません。

GitHub Actionsは公開リポジトリ用の標準Ubuntuランナーで実行します。有料ランナー、Codespaces、Actionsキャッシュ、成果物ストレージは使わず、APKはGitHub Releasesに公開しています。

## 位置情報とAI送信

位置情報は検索ボタンを押した時だけ取得し、距離計算は端末内で行います。Geminiへ送るのは公開RSSのイベント情報で、利用者の緯度・経度は送信しません。無料枠の入力内容と応答は、Googleによる確認やモデル改善の対象になることがあります。Gemini APIの利用条件に合わせ、成人向けの利用を想定しています。

## ソース

- [完全なFlutterプロジェクトZIP](https://github.com/akari828-prog/nearby-leisure-finder-demo/blob/main/nearby_leisure_finder_flutter.zip)
- [スマホ向け手順](https://github.com/akari828-prog/nearby-leisure-finder-demo/blob/main/README_PHONE_JA.md)
- [ビルド設定と費用の説明](https://github.com/akari828-prog/nearby-leisure-finder-demo/blob/main/README_FREE_BUILD_JA.md)
- [APKビルド履歴](https://github.com/akari828-prog/nearby-leisure-finder-demo/actions/workflows/build-apk.yml)