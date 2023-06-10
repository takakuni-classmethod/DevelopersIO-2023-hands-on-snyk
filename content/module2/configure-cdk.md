# AWS CDK の設定

> **Note**
> 
> ここで定義する手順は、ワークショップに進む前に実行する必要があります。ワークショップ中に AWS リソースのデプロイで問題が発生した場合は、ここに戻ってください。

このセクションでは、AWS CDK 環境を設定を行います。

1\. AWS Cloud9 に進み、ターミナルウィンドウに次のコマンドを入力します。

```bash
cd ~/environment/DevelopersIO-2023-hands-on-snyk-cdk/pipeline
```

2\. Cloud9 にプリインストールされた Python ライブラリを維持するために、プロジェクト専用の仮想 Python 環境を作成することを強くお勧めします。仮想環境を作成するには、Cloud9 ターミナルウィンドウに次のコマンドを入力します。

```bash
python3 -m venv .venv
```

3\. 仮想環境をアクティベートします

```bash
source .venv/bin/activate
```

> **Note**
> 
> AWS アカウントからログアウトし、AWS Cloud9 をリロードした場合には、この仮想環境を使用することを Python に明示的に指定するため、手順 3 を再実行してください。

4\. 仮想環境がアクティブになると、現在のターミナルセッションが仮想環境を使用していることが示されます (シェルの左端に `.venv` と示されています)。 

<img src="/static/images/module2/02-01-configure-cdk.png" width=100%>

5\. 次のコマンドで必要なライブラリをインストールしましょう。

```bash
pip install -r requirements.txt
```

パイプラインとツールのデプロイに進みます。

[Next: パイプラインとツールのデプロイ](./deploy-pipeline.md)