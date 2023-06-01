# パイプラインとツールのデプロイ

CDK 環境ができたので、リリースパイプラインをデプロイします。

1\. AWS Cloud9 のターミナルウィンドウに戻り、**pipeline** フォルダの下の **config.yaml.sample** から **config.yaml** という名前の新しいファイルを作成しましょう。

```bash
cd ~/environment/pipeline
cp config.yaml.sample config.yaml
```

2\. 左側にある Cloud9 のエクスプローラーをクリックして、新しく作成したファイル (**config.yaml**) を開きます。

<img src="/static/images/module2/02_configure-cdk.png">

3\. **config.yaml** は、ワークショップ中にパイプラインで特定のビルドステージを有効/無効にします。現状、それらのほとんどは有効になっています（`enabled: True` と記述されています）。 ここでは、このファイルに変更を加えることはありません。 この時点で、**config.yaml**は次のようになっているはずです。

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
  enabled: True

### Dynamic Application Security Testing (DAST) Step
dast:
  enabled: False
  zaproxy:
    instance_type: t3.medium
    api_key: SomeRandomString
```

4\. CDK コマンドを実行する前に、CDK がデプロイするために必要なリソース をプロビジョニングしましょう。Cloud9 ターミナルに以下を入力するだけで、プロビジョニング出来ます

```bash
cdk bootstrap
```

4\. 次に、CDK が正しくインストールされ、構成されているかどうかをテストしましょう。 Cloud9 のターミナルで以下のコマンドを入力します。リリースパイプライン構築のための結合された CloudFormation テンプレートが表示されるはずです。

```bash
cdk synth
```

6\. Cloud9 のターミナルウィンドウで、以下のコマンドでリリースパイプラインをデプロイしてみましょう。

```bash
cdk deploy --require-approval never
```

7\. CDK のデプロイを数分待ってみましょう。AWS リソースのプロビジョニング中に、(**pipeline/appsec_workshop** フォルダーの下) CDK コンストラクトのいくつかを調べてみましょう。CDK が完了すると、次の出力が得られるはずです。

次のセクションに進み、展開した内容を調べてください。

[Next](../module2/configure-cdk.md.md)