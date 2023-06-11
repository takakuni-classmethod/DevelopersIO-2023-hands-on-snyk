# ECS タスクの更新

Web アプリケーションの修正が完了したため、ビルドされたコンテナイメージを ECS に適用します。

1\. **DevelopersIO-2023-hands-on-snyk-cdk/pipeline/config.yaml** を次のように変更します。

```yaml
### Staging Auto-Deploy
auto_deploy_staging: True
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

2\. 修正が完了したら次のコマンドでパイプラインの更新を行います。

```bash
cd ~/environment/DevelopersIO-2023-hands-on-snyk-cdk/pipeline
cdk deploy --require-approval never
```

> **Note**
> 
> AWS アカウントからログアウトし、AWS Cloud9 をリロードした場合には、仮想環境を再度有効化する必要があるため、`cdk deploy` 前に、 `source .venv/bin/activate` を実行してください。

3\. デプロイが完了すると、次のような出力が得られるはずです。

<img src="/static/images/module6/01-01-update-ecs-task.png" width=100%>

4\. CodePipeline コンソールでも、 **DeployToStaging** ステージが追加されていることがわかります。

<img src="/static/images/module6/01-02-update-ecs-task.png" width=100%>

5\. パイプラインの更新を行ったため、 CodePipeline コンソールから **[変更をリリース]** をクリックして、 ECS タスクの置き換えを行います。

<img src="/static/images/module6/01-03-update-ecs-task.png" width=100%>

6\. 確認画面が出てくるので **[リリースする]** をクリックします。

<img src="/static/images/module6/01-04-update-ecs-task.png" width=100%>

7\. パイプラインの実行が完了すると、 ECS タスクの置き換えが完了します。

<img src="/static/images/module6/01-05-update-ecs-task.png" width=100%>

[Next: 修正プログラムの検証](./validate-fixes.md)