# 近くで、ちょっと遊ぼう。

現在地の近くで遊び・レジャーのイベント候補を探すAndroidアプリです。スマートフォンだけでインストールできます。

## 今すぐインストール

[Android free build 7 のAPKをダウンロード]( https://github.com/akari828-prog/nearby-leisure-finder-demo/releases/download/android-free-37396900610-1/nearby-leisure-free.apk )

ファイルサイズは約48.7 MB、SHA-256は **4c00ff0eb58a6473c7ad805b919acac78a9cc6cdd09636a0ce401154c8cde0a5** です。

1. Androidスマートフォンで上のリンクを開いてAPKをダウンロードします。
2. ダウンロード通知または「Files」アプリからAPKを開きます。
3. Androidが求めた場合、APKを開いたブラウザーまたはファイルアプリに「この提供元のアプリを許可」を設定します。
4. 「インストール」を押します。

## 確認状況

GitHub Actionsでflutter pub get、flutter analyze、flutter test、Release APKビルド、署名検証、Release登録が成功しました。実機へのインストールと起動はまだ確認できていません。

以前のGemini実検索版は配布停止し、APKをリリースから外しました。Gemini Developer APIの現行追加利用規約では一般消費者向けアプリでの利用が認められていないためです。詳しくは[Googleの利用規約](https://ai.google.dev/gemini-api/terms)を確認してください。

## この無料版について

- RSSから最大10件の候補を取得し、端末内のキーワードでイベント分類
- RSSに書かれた住所だけを使って距離を計算し、10km以内を近い順に表示
- GPSは検索ボタンを押した時だけ取得し、距離計算は端末内で実行
- Firebase、Gemini API、APIキー、支払い方法は不要
- Google公式テスト広告IDを使用

キーワード判定には誤判定や見逃しがあります。RSSに場所や日時が書かれていない場合は補いません。検索結果はRSS提供元の更新状況に左右されます。

## ソース

- [完全なFlutterプロジェクト](https://github.com/akari828-prog/nearby-leisure-finder-demo/blob/main/nearby_leisure_finder_flutter.zip)
- [スマートフォン向け手順](README_PHONE_JA.md)
- [無料ビルドの説明](README_FREE_BUILD_JA.md)
