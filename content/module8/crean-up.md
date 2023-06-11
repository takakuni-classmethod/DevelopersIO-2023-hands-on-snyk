# 片付け

このワークショップで利用したリソースの削除を行います。

1\. AWS コンソールに **ECR** と入力して、 ECR コンソールを開きます。 **flask-app** プライベートリポジトリを選択し、削除をクリックします。確認画面で delete と入力し、次のステップに進みます。

<img src="/static/images/module8/01-01-crean-up.png" width=100%>

2\. AWS Cloud9に戻り、以下のコマンドを入力して、このワークショップでプロビジョニングしたものをすべて破棄します。

```bash
cd ~/environment/DevelopersIO-2023-hands-on-snyk-cdk/pipeline
cdk destroy
```

> **Note**
> 
> AWS アカウントからログアウトし、AWS Cloud9 をリロードした場合には、仮想環境を再度有効化する必要があるため、`cdk destroy` 前に、 `source .venv/bin/activate` を実行してください。

3\. **cdk destroy** がタスクを完了したら、必要に応じて AWS Cloud9 環境を削除します。Cloud9 Console に移動し、 Cloud9 環境を選択して、 Delete をクリックします。

<img src="/static/images/module8/01-02-crean-up.png" width=100%>

4\. Cloud9 側の CloudFormation スタックも削除しておきましょう。 CloudFormation コンソールに移動し、 Cloud9 作成時に自動で作成された CloudFormation スタックを選択します。 **[削除]** をクリックして、スタックの削除を行います。

<img src="/static/images/module8/01-03-crean-up.png" width=100%>

5\. CodeBuild のロググループを削除します。 CloudWatch コンソールからロググループを選択し、今回作成した CodeBuild プロジェクトのロググループを選択します。 **[ロググループの削除]** をクリックし、ログを削除します。

<img src="/static/images/module8/01-04-crean-up.png" width=100%>

6\. AWS CDK で利用した CloudFormation テンプレートを削除します。 S3 コンソールに移動し、 **cdk-ランダム文字列-assets-アカウントID-リージョン** のバケットをクリックします。

<img src="/static/images/module8/01-05-crean-up.png" width=100%>

7\. 今日付けで作成されたオブジェクトを選択し、**[削除]** をクリックします。

> **Warning**
> 共通アカウントなど、ワークショップの同じ時間帯に、自分以外が CDK デプロイしている可能性がある場合、削除対象のオブジェクトをダウンロードしてみて、CDK でデプロイしたリソースと相違がないか確認してください。

<img src="/static/images/module8/01-06-crean-up.png" width=100%>

8\. テキスト入力フィールドに **削除** と入力し、 **[オブジェクトの削除]** をクリックします。

<img src="/static/images/module8/01-07-crean-up.png" width=100%>

9\. バージョニングが有効になっているため、オブジェクトを完全に削除できていません。オブジェクトを完全に削除するには **[バージョンの表示]** をクリックし、削除マーカーと手順 8 で削除したオブジェクトを選択します。オブジェクトを選択後、**[削除]** をクリックします。

<img src="/static/images/module8/01-08-crean-up.png" width=100%>

10\. テキスト入力フィールドに **完全に削除** と入力し、 **[オブジェクトの削除]** をクリックします。

<img src="/static/images/module8/01-09-crean-up.png" width=100%>

11\. CodePipeline で利用したアーティファクト保管用 S3 バケットを削除します。 S3 コンソールに移動し、バケットのフィルターから **appsecworkshopstack-pipelineartifactsbucket** と検索します。 バケットを選択後、オブジェクトを削除するため **[空にする]** を選択します。

<img src="/static/images/module8/01-10-crean-up.png" width=100%>

12\. テキスト入力フィールドに **完全に削除** と入力し、 **[空にする]** をクリックします。 **[終了]** をクリックします。

<img src="/static/images/module8/01-11-crean-up.png" width=100%>

13\. もう一度、バケットのフィルターから **appsecworkshopstack-pipelineartifactsbucket** と検索します。バケットを選択後、 **[削除]** をクリックします。

<img src="/static/images/module8/01-12-crean-up.png" width=100%>

14\. テキスト入力フィールドにバケットの名前を入力し、**[バケットの削除]**をクリックします。

<img src="/static/images/module8/01-13-crean-up.png" width=100%>