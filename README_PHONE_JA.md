# PCなし・課金なしでAndroidに入れる手順

この説明書の時点ではAPKはまだ生成されていません。Flutterプロジェクトとクラウドビルドの準備を完了しています。

## 最初の確認

公開GitHubリポジトリの標準ランナーでビルドし、生成したAPKをGitHub Releasesで配布する構成です。アプリのソースとテスト用APKは公開されます。公開の許可を得た後に、新しいリポジトリを作成してビルドします。

GitHubのリポジトリ作成とSecrets登録にはブラウザ操作が必要です。GitHubのログインが必要になった場合は本人の操作で認証します。GitHubの有料ランナー、Codespaces、Actionsのキャッシュや成果物ストレージは使いません。

## 無料のGeminiで実際のイベントを検索する準備

1. スマホのブラウザで https://console.firebase.google.com/ を開きます。
2. このアプリ用にFirebaseプロジェクトを作成し、無料の **Sparkプラン** を維持します。Cloud Billingの請求先アカウントを紐付けず、支払い方法を登録しません。
3. プロジェクトにAndroidアプリを追加します。パッケージ名は **jp.example.nearbyleisurefinder** です。表示名は **近くで、ちょっと遊ぼう。** にできます。
4. Androidアプリ登録後の **google-services.json** をダウンロードします。このファイルをChatGPTへ添付すれば、Firebase登録情報をクラウドビルドへ設定できます。パスワード、Gemini APIキー、サービスアカウント秘密鍵は不要です。
5. Firebase Consoleで **Firebase AI Logic** を開始し、バックエンドは **Gemini Developer API** を選びます。有料のバックエンドやBlazeプランへの変更は選びません。モデルは **gemini-3.5-flash-lite** を使います。
6. FirebaseのAndroidアプリ設定と **App Check** に次の公開署名フィンガープリントを登録します。これは、このアプリ用に準備した固定の端末確認用署名鍵の情報です。

   **SHA-1**

   ~~~text
   54:EE:91:10:BA:67:5C:ED:D1:1E:B3:F2:E6:28:27:E0:34:1B:D2:36
   ~~~

   **SHA-256**

   ~~~text
   4B:A0:A8:D9:E7:14:3A:E5:F5:93:9B:BB:44:58:B7:8A:57:C1:C1:9D:C7:2C:72:F4:D5:6F:72:1D:C8:B7:A9:95
   ~~~

7. App CheckのAndroidプロバイダは **Play Integrity** を使います。APKを直接配布する場合は、公式資料の「Google Play以外に限定」に合わせ、**PLAY_RECOGNIZED不要、LICENSED不要、デバイスの完全性を要求**する設定を使います。Google Play Console側でのAPI・Cloudプロジェクトの設定が必要になる場合があります。無料での設定が完了しない場合は、課金手続きをせず、その画面で停止して確認します。
8. 実機からApp Checkの有効なリクエストが届くことを確認し、Firebase AI LogicのApp Check適用を有効にします。公開配布前に未登録端末からのアクセスが拒否されることも確認します。

FirebaseのAndroid APIキーはFirebaseプロジェクトの識別情報で、サービスアカウント秘密鍵やGemini APIキーとは異なります。このアプリはGemini APIキーをDartへ埋め込みません。Firebaseの設定ファイルはGitHub Secretsで渡し、ソースへコミットしません。

## ビルドからインストール

Firebase設定前でも、mockモードで表示・距離・広告・ブラウザ遷移を確認するAPKを作れます。実際の検索にはFirebaseとApp Checkの設定が必要です。

Firebaseの設定後にActionsの **Build free Android APK** を **live** で実行します。依存取得、静的解析、APK生成が順番に実行されます。失敗した場合はエラーログを確認して修正し、ビルドが成功してからAPKを案内します。

1. GitHub Releasesにある **nearby-leisure-live.apk** をスマホにダウンロードします。デモ版は **nearby-leisure-mock.apk** です。
2. ダウンロードしたAPKを開きます。
3. Androidが求めた場合だけ、APKを開いたアプリに「この提供元のアプリを許可」のインストール権限を付けます。
4. 「インストール」を押します。
5. アプリを起動し、「現在地から探す」を押した時に位置情報を許可します。

アプリは常時・バックグラウンドの位置取得を行いません。Geminiへ現在地の緯度・経度は送りません。無料枠の上限に達したら検索エラーとなり、再検索できます。課金プランへの自動切り替えはありません。

## 公式資料

確認日：2026年10月5日。

- Firebase AI Logicの無料枠：https://firebase.google.com/docs/ai-logic/pricing?hl=ja
- Geminiのモデル別料金：https://ai.google.dev/gemini-api/docs/pricing
- FirebaseのAPIキー：https://firebase.google.com/docs/projects/api-keys?hl=ja
- Play IntegrityとApp Check：https://firebase.google.com/docs/app-check/android/play-integrity-provider?hl=ja
- GitHub Actionsの料金：https://docs.github.com/en/billing/concepts/product-billing/github-actions
- GitHub Releases：https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases
