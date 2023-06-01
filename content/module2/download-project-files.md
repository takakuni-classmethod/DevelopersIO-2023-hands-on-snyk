# Project File のダウンロード

このワークショップのリリースパイプラインの必要なリソースはすべてAWS CDK で定義されています。

このタスクでは、ソースコードの一式を Cloud9 環境にダウンロードします。

1\. AWS Cloud9 に進み、ターミナルウィンドウに入り、次のコマンドを貼り付けて、コードをダウンロードします。

```
curl 'https://static.us-east-1.prod.workshops.aws/public/34501f9e-b048-471f-a9e7-343b5cf15426/assets/pipeline.zip' --output pipeline.zip
unzip pipeline.zip -d pipeline && rm pipeline.zip
```

2. リリース自動化用の CDK コンストラクトを含む **pipeline** という名前の新しいフォルダが表示されます。次のセクションに進み、環境にデプロイしましょう。

<img src="/static/images/module2/01_download-project-files.png" width="100%">

