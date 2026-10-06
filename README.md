# 近くで、ちょっと遊ぼう。

現在地の近くで遊び・レジャーのイベント候補を探すAndroidアプリです。スマートフォンだけで入れられるAPKをGitHub Actionsでビルドします。

## 配布状況

以前のGemini実検索版は配布を停止しました。Gemini Developer APIの現行追加利用規約が一般消費者向けアプリでの利用を認めていないためです。古い「mock」版も実際の開催情報を表示しません。

現在、Firebase・Gemini・APIキー・支払い設定を使わない無料版へ切り替えています。RSSの情報を端末内のキーワードで判定して距離順に表示します。ビルドが完了すると、[Releases](https://github.com/akari828-prog/nearby-leisure-finder-demo/releases) に **Android free build** が現れます。ここにAPKがまだ表示されない間は、新しいビルドの準備中です。

## スマートフォンへのインストール

1. スマートフォンで [Releases](https://github.com/akari828-prog/nearby-leisure-finder-demo/releases) を開きます。
2. 最新の **Android free build** を選びます。
3. nearby-leisure-free.apk をダウンロードして開き、Androidの案内に従ってインストールします。

実機でのインストールと起動は確認前のため、確認状況はリリース説明に記載します。デモ版や「配布停止」と表示されたAPKは実検索版ではありません。

## 無料版の機能

- RSSの公開情報から最大10件のイベント候補を取得
- 祭り、マルシェ、展示、観光などのキーワードを端末内で判定
- RSSに書かれた住所だけをジオコーディングし、10km以内を距離順で表示
- GPSは検索を押した時だけ取得し、距離計算は端末内で実行
- Google公式テスト広告を使用し、3回目ごとのタップだけ広告表示対象

キーワード判定には誤判定や見逃しがあります。RSSに場所や日時が書かれていない場合は補いません。RSS提供元の利用条件に従い、元記事リンクと短い説明を表示します。

## 開発情報

完全なFlutterプロジェクトは [nearby_leisure_finder_flutter.zip](https://github.com/akari828-prog/nearby-leisure-finder-demo/blob/main/nearby_leisure_finder_flutter.zip) です。実行、RSS、広告の設定は [日本語README](README_JA.md)、スマートフォンの手順は [README_PHONE_JA.md](README_PHONE_JA.md) を参照してください。
