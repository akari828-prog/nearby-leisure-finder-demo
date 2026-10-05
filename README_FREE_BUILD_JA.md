# PCなし・無料でAndroid APKを作るプロジェクト

## 状態

公開リポジトリを作成し、デモAPKを生成しました。依存取得、flutter analyze（指摘0件）、リリースAPK生成、apksignerでの署名検証、GitHub Releasesへの公開が成功しています。

**APKのダウンロードページ**：https://github.com/akari828-prog/nearby-leisure-finder-demo/releases/tag/android-mock-37264135261-1

**リポジトリ**：https://github.com/akari828-prog/nearby-leisure-finder-demo

Firebaseプロジェクト **nearby-leisure-finder** をSparkプランで作成し、Androidアプリと固定署名のフィンガープリントを登録しました。固定署名鍵のGitHub Secretも登録済みです。実検索APKは未生成で、実機起動は未確認です。実検索の設定にはGemini APIとPlay Integrity APIの追加規約への本人の同意、およびFirebaseのAndroid構成ファイルが必要です。

## 課金を避ける設定

- ビルドジョブは akari828-prog の公開リポジトリでのみ起動します。非公開リポジトリではスキップします。
- ubuntu-24.04 の標準GitHubホストランナーを使用します。
- 有料の大型ランナー、カスタムイメージ、Codespaces、キャッシュ機能は使用しません。
- Actionsの成果物ストレージにはAPKを保存しません。GitHub Releasesの公開ダウンロードファイルとして保存します。
- FirebaseはSparkプランのまま使い、Cloud Billingの請求先アカウントを紐付けません。

GitHub公式の料金説明とReleasesの説明：

- https://docs.github.com/en/billing/concepts/product-billing/github-actions
- https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases

## ファイル

| ファイル | 内容 |
| --- | --- |
| nearby_leisure_finder_flutter.zip | Flutterアプリの完全なソース。pubspec、全Dartファイル、Android設定、Gradle wrapper、Firebase設定変換ツール、READMEを含みます。 |
| SOURCE_SHA256.txt | ソースZIPの整合性確認用ハッシュ。 |
| .github/workflows/build-apk.yml | 依存取得、flutter analyze、デモまたは実検索APK生成、ReleasesへのAPK登録を自動実行します。 |
| README_FREE_BUILD_JA.md | この説明書。 |
| README_PHONE_JA.md | スマホでのFirebase設定とAPKインストール手順。 |

## ビルドの手順

1. 上記のAPKダウンロードページをスマホで開きます。
2. Assets の **nearby-leisure-mock.apk** をダウンロードします。ZIPを展開する必要はありません。
3. APKを開き、「インストール」を選択します。Androidが求めた場合は、APKを開いたアプリにインストールを許可します。
4. デモの「現在地から探す」を押して、サンプル一覧を確認します。

ソースZIP、ハッシュ、ワークフローの変更をGitHubへ追加するとmockビルドが自動実行されます。Actionsの手動実行でもmock/liveを選べます。

GitHub接続が利用できる場合、リポジトリへのファイル追加、ビルド確認、エラーログ取得、修正は自動で進められます。Secrets登録とFirebaseの設定はブラウザで行います。ログインが必要な場合は本人の操作で認証します。

## 固定署名鍵

更新インストールとApp Checkの証明書登録には、毎回同じ署名鍵を使います。別ファイル **nearby_leisure_signing_backup.zip** に、このアプリ用に作成した端末確認用の鍵と復旧手順を保管しています。署名鍵はソースZIPや公開リポジトリへ含めません。

GitHubリポジトリの Settings → Secrets and variables → Actions に、Repository secret **ANDROID_DEBUG_KEYSTORE_BASE64** を登録します。値は署名バックアップ内の **ANDROID_DEBUG_KEYSTORE_BASE64.txt** の内容です。ワークフローはこの鍵をRunner内に復元します。

固定鍵が未登録のmockビルドは、一時的なDebug署名で生成できます。そのAPKの証明書はREADME_PHONE_JA.mdのフィンガープリントと一致しません。後で固定鍵のAPKへ切り替える場合は、先のアプリをアンインストールして入れ直してください。liveビルドでは固定鍵のSecretが必須です。

この鍵は端末確認用です。Google Play公開用の署名ではありません。公開用の署名設定は README_JA.md に従って別途設定します。

## デモAPKの動作

push時と手動実行の初期選択はmockです。東京駅を基準とするサンプルイベント、距離表示、3回ごとの広告表示対象ルール、ブラウザ遷移を確認します。
Firebaseの初期化、Gemini呼び出し、実RSSの取得、スマホの現在地取得は実行されません。Google公式テスト広告IDを使います。サンプルは実在の開催情報ではありません。

## 無料のGeminiを使う実検索APK

Firebaseは無料の **Sparkプラン** にし、**Cloud Billingの請求先アカウントを紐付けません**。Firebase AI Logicでは **Gemini Developer API** バックエンドを使います。ソースの **FirebaseAI.googleAI()** がこのバックエンドです。

**lib/config/ai_config.dart** の初期モデル **gemini-3.5-flash-lite** は、2026年10月5日時点でテキスト入力・出力の無料枠があります。検索1回につき最大10件を1回のAIリクエストにまとめ、同じ入力の結果はアプリ起動中のキャッシュを再利用します。上限に達したら検索エラーとして表示します。課金への自動切り替えやAIの自動再試行はありません。アプリ自身はプロジェクトの請求設定を検査・変更しません。

1. **README_PHONE_JA.md** に従ってFirebaseのAndroidアプリ、AI Logic、App Checkを設定します。
2. Firebaseからダウンロードした **google-services.json** の内容をRepository secret **FIREBASE_GOOGLE_SERVICES_JSON** に登録します。Gemini APIキーやサービスアカウント秘密鍵は登録しません。
3. 固定署名鍵のSecretを登録します。
4. GitHubのActionsで **Build free Android APK** → Run workflowを選び、modeを **live** にして実行します。
5. ワークフローがgoogle-services.jsonの登録内容を検証し、ビルド定義へ変換します。コードを手で書き換えたり、PCでFlutterFire CLIを実行したりする必要はありません。
6. 成功したReleasesから **nearby-leisure-live.apk** をダウンロードします。

不正なJSON、別アプリのパッケージ名、Firebase設定不足、固定署名鍵不足の場合は、実検索版のビルドをエラーで停止します。デモとして成功扱いにはしません。

モデルを変更する前にも無料枠の対象を確認してください。

- https://firebase.google.com/docs/ai-logic/pricing?hl=ja
- https://ai.google.dev/gemini-api/docs/pricing

FlutterFire CLIでの設定方法と実行コマンドは、ソースZIP内の **README_JA.md** に記載しています。
