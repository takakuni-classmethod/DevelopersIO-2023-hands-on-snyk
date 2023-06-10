# パイプラインとツールのデプロイ

AWS CDK のセットアップが完了したため、リリースパイプラインをデプロイします。

今回の AWS CDK で以下のリソースをデプロイします。後続の AWS Fargate へのデプロイフローは、現時点では作成しません。

<img src="/static/images/module2/02-01-deploy-pipeline.png" width=100%>

1\. AWS Cloud9 のターミナルウィンドウに戻り、 **DevelopersIO-2023-hands-on-snyk-cdk/pipeline** フォルダの下の **config.yaml.sample** から **config.yaml** という名前の新しいファイルを作成しましょう。

```bash
cd ~/environment/DevelopersIO-2023-hands-on-snyk-cdk/pipeline
cp config.yaml.sample config.yaml
```

2\. 左側にある Cloud9 のエクスプローラーをクリックして、新しく作成したファイル (**config.yaml**) を開きます。

<img src="/static/images/module2/02-02-deploy-pipeline.png" width=100%>

3\. このワークショップでは **config.yaml** を利用してパイプラインの特定のビルドステージを有効/無効にする仕組みになっています。

```yaml
### Staging Auto-Deploy
auto_deploy_staging: False
initial_image: public.ecr.aws/adelagon/flask-app:latest

### Static Application Security Testing (SAST) Step
sast:
  enabled: True

### Software Composition Analysis (SCA) Step
sca:
  enabled: True

### License Checker Step
license:
  enabled: False

### Dynamic Application Security Testing (DAST) Step
dast:
  enabled: False
  zaproxy:
    instance_type: t3.medium
    api_key: SomeRandomString
```
4\. AWS CDK では `cdk` コマンドを実行する前に、CDK を利用するために必要なリソースをプロビジョニング（[ブートストラッピング
](https://docs.aws.amazon.com/ja_jp/cdk/v2/guide/bootstrapping.html)）する必要があります。 Cloud9 ターミナルに以下のコマンドを入力するだけで、プロビジョニング出来ます。

```bash
cdk bootstrap
```

5\. 次に、CDK が正しくインストールされ、構成されているかどうかをテストしましょう。Cloud9 のターミナルで以下のコマンドを入力します。リリースパイプライン構築のための結合された CloudFormation テンプレートが表示されるはずです。

```bash
cdk synth
```

6\. Cloud9 のターミナルウィンドウで、以下のコマンドでリリースパイプラインをデプロイしてみましょう。

```bash
cdk deploy --require-approval never
```

7\. CDK のデプロイを数分待ってみましょう。 AWS リソースのプロビジョニング中に、（**DevelopersIO-2023-hands-on-snyk-cdk/pipeline/appsec_workshop** フォルダーの下）CDK コンストラクトのいくつかを調べてみましょう。CDK が完了すると、次のような出力が得られるはずです。

<img src="/static/images/module2/02-03-deploy-pipeline.png" width=100%>

次のセクションに進み、展開した内容を調べてください。

[Next: 構築された環境の確認](./explore-the-environment.md)