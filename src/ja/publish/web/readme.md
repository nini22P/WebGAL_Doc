# Web ウェブ

## **エディタ** を使用している場合

エディタの右上にある「Web にエクスポート」を選択します。Web のデプロイ方法は、通常の Web サイトをデプロイする方法と変わりません。クラウドサーバー（Tencent Cloud、Alibaba Cloud など）を購入してデプロイするか、GitHub Pages を使用することができます。

## **リリース版** を使用している場合

/WebGAL の下にあるファイル（フォルダではなく、/WebGAL フォルダの下にあるファイル）を、デプロイしたいクラウドサーバーの指定されたディレクトリにコピーするか、GitHub Pages にデプロイします。

## **ソースコード開発** を使用している開発者

ソースコードを使用してデバッグを行う場合、`yarn build` を使用して静的 Web ページ（packages/webgal/dist フォルダ内）を作成し、このフォルダ内のコンテンツを GitHub Pages またはクラウドサーバーにデプロイすることができます。