# スマホだけで実検索版をインストールする手順

## 今すぐ入れる

[実検索版APK（Android live build 6）を開く](https://github.com/akari828-prog/nearby-leisure-finder-demo/releases/tag/android-live-37393697758-1)

このAPKは50.3 MBです。SHA-256: `c34ba49f85f5bdba0b63753e201ccf3de007a61b45c135f0ba3c46b922685724`

1. Androidスマートフォンで上のリンクを開き、Assetsから **nearby-leisure-live.apk** をタップします。
2. ダウンロードが終わったら、ブラウザーの「開く」を押すか、「ファイル」アプリのダウンロード一覧からAPKを開きます。
3. Androidが確認を出した場合だけ、APKを開いたブラウザーまたはファイルアプリに「この提供元のアプリを許可」を設定します。
4. インストール画面で「インストール」を押します。
5. アプリを起動し、「現在地から探す」を押した時に位置情報を許可します。

位置情報は検索時だけ取得します。バックグラウンドでは取得しません。Geminiには位置情報を送らず、現在地からの距離は端末で計算します。

ビルド5のデモAPKとビルド6は同じ署名鍵なので、そのまま更新できます。ビルド4のAPKだけは別鍵で署名されています。ビルド4を使っている場合は、いったんアンインストールしてからビルド6を入れてください。

## 完了した設定

- Firebaseプロジェクト **nearby-leisure-finder** はSparkプラン（無料）です。Cloud Billingの請求先、支払い方法は登録していません。
- Firebase AI Logicで無料の **Gemini Developer API** を有効化しました。任意のAI Monitoringはオフです。モデルは `lib/config/ai_config.dart` の `gemini-3.5-flash-lite` です。
- Firebase App CheckのAndroidプロバイダを **Play Integrity** に登録しました。Google Play経由でないAPKに合わせて **PLAY_RECOGNIZED** と **LICENSED** は必須にせず、デバイスの完全性は要求します。
- SHA-256署名フィンガープリントは、APK署名検証結果とFirebase登録値が一致しています。
- SDKの設定取得用に同じFirebaseプロジェクトへ「SDK設定取得用」Webアプリを登録しました。Firebase Hostingは有効にしていません。
- Firebaseのビルド設定と署名鍵はGitHubの非公開Actions Secretsに保存し、公開ソースには含めていません。Gemini APIキーやサービスアカウント鍵は使っていません。

## ビルド検証

GitHub Actionsで **flutter pub get**、**flutter analyze**、実検索版 **flutter build apk --release**、APK署名検証、GitHub Releasesへの公開が成功しました。実機へのインストールと起動確認はまだできていません。

APK署名情報:

~~~text
SHA-1   54:EE:91:10:BA:67:5C:ED:D1:1E:B3:F2:E6:28:27:E0:34:1B:D2:36
SHA-256 4B:A0:A8:D9:E7:14:3A:E5:F5:93:9B:BB:44:58:B7:8A:57:C1:C1:9D:C7:2C:72:F4:D5:6F:72:1D:C8:B7:A9:95
~~~

## 料金とAIデータ

Firebaseプロジェクトに請求先を登録していないため、Geminiの無料枠上限に達した場合は検索エラーになります。無料枠には回数制限があり、課金プランへ自動切り替えしません。広告はGoogle公式テスト広告IDを使います。

無料枠では送信したRSS本文とAI応答がGoogleの確認や製品改善の対象になることがあります。Gemini APIの利用条件に合わせ、このアプリは18歳以上向けとして扱ってください。GeminiにはRSS由来のイベント情報だけを送り、位置情報・緯度・経度は送りません。

## ソースと手順

- [Flutterプロジェクトの完全なソースZIP](https://github.com/akari828-prog/nearby-leisure-finder-demo/blob/main/nearby_leisure_finder_flutter.zip)
- [ビルドと無料設定の説明](https://github.com/akari828-prog/nearby-leisure-finder-demo/blob/main/README_FREE_BUILD_JA.md)
- [GitHubリポジトリ](https://github.com/akari828-prog/nearby-leisure-finder-demo)