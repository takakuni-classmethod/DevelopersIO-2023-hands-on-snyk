# 構築された環境の確認

先に進む前に、AWS CDK がプロビジョニングした内容について理解しておきましょう。

1\. AWS コンソールの検索バーに **CodeCommit** と入力して AWS CodeCommit ダッシュボードを開き、**flask-app** という名前の Git リポジトリが作成されたことを確認します。このリポジトリではウェブアプリケーションのコードが管理されますが、現時点では**何のファイルも入っていない空のリポジトリ**です。また、 **CloudWatch Event Rule** を作成して、開発者がコードを push するたびにリリースパイプラインがトリガーされるように設定しています。

<img src="./../../static/images/module2/02-01-explore-the-environment.png" width="100%">

2\. 次に、リリースパイプラインがどのように見えるか見てみましょう。左側のメニューから **[パイプライン]** の下の **[パイプライン]** をクリックします。

**devsecops-pipeline** という名前の新しいパイプラインがあるはずです。 CodeCommit リポジトリは現時点で空であるため、失敗と表示されているのは想定通りです。

<img src="./../../static/images/module2/02-02-explore-the-environment.png" width="100%">

3\. Pipelinesのリストから **devsecops-pipeline** をクリックすると、 3 つのステージがあることがわかるはずです。**CheckoutSource** ステージは、CodeCommit リポジトリにコードの変更があるたびにトリガーされます。

また、 **ApplicationSecurityChecks** というステージがあり、SAST, Licenses というアクションが含まれていることにお気づきでしょうか。これらのアプリケーションセキュリティチェックは互いに依存しないため、パイプラインを高速化するため並行して実行することは合理的です。

AWS CodePipeline では、パイプライン構造で [runOrder](https://docs.aws.amazon.com/ja_jp/codepipeline/latest/userguide/reference-pipeline-structure.html) を指定することで、並行してアクションを実行できます。 セキュリティチェックがすべて合格したら、 **BuildImage** ステージを実行し、 Web アプリケーションのコンテナイメージを作成します。

<img src="./../../static/images/module2/02-03-explore-the-environment.png" width="100%">

**BuildImage** ステージを定義する CodeBuild プロジェクトを確認してみましょう。

4\. マネジメントコンソールの 検索バーに **CodeBuild** と入力し、CodeBuild を選択すると AWS CodeBuild のダッシュボードが表示されます。 **codebuild-docker-project** という名前の CodeBuild プロジェクトが表示されているはずです。

<img src="./../../static/images/module2/02-04-explore-the-environment.png" width="100%">

5\. CodeBuild プロジェクトが実際に行っていることを詳しく知るには、 Build プロジェクト一覧から **codebuild-docker-project** をクリックし、 **ビルドの詳細** タブをクリックします。

<img src="./../../static/images/module2/02-05-explore-the-environment.png" width="100%">

6\. ビルドの詳細ページを下にスクロールすると、 **Buildspec** セクションに **docker_buildspec.yaml** の現在の値が表示されています。 **[Buildspecs](https://docs.aws.amazon.com/ja_jp/codebuild/latest/userguide/build-spec-ref.html)** は、 CodeBuild がビルドを実行するために使用するビルドコマンドと環境変数などを設定するファイルです。このラボでは、 buildspecs は コードベース (CodeCommit) から取得することになります。 CodeBuild は Web アプリケーションのコードから docker_buildspec.yaml という名前のファイルを探し、それを実行します。このモジュールの「APPENDIX: Exploring docker_buildspec.yaml」セクションで、このことを詳しく調べます。