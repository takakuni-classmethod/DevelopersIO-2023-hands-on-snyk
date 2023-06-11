# APPENDIX: マネージド Snyk アクションの組み込み

Snyk Open Source は AWS CodePipeline とマネージドに統合しています。

このセクションでは、マネージドアクションを利用して、Snyk Open Source の結果をよりみやすくレポートしていきます。

1\. **devsecops-pipeline** を編集していきます。 CodePipeline コンソールで **[編集する]** をクリックします。

<img src="/static/images/module7/01-01-managed-snyk-action.png" width=100%>

2\. **ApplicationSecurityChecks** ステージの **[ステージの編集]** をクリックします。

<img src="/static/images/module7/01-02-managed-snyk-action.png" width=100%>

3\. **アクションの追加** から、Snyk アクションを追加します。パラメーターは以下を入力・選択してください。

- アクション名：SCA_Managed_Snyk_Action
- アクションプロバイダー：Snyk
- 入力アーティファクト：Artifact_CheckoutSource_CodeCommit
- 出力アーティファクト：Artifact_ApplicationSecurityChecks_SCA_Managed_Snyk

<img src="/static/images/module7/01-03-managed-snyk-action.png" width=100%>

4\. **[Snyk に接続]** をクリックします。認証画面に遷移した方は、サインアップした方法で再度 Snyk へログインしてください。

<img src="/static/images/module7/01-04-managed-snyk-action.png" width=100%>

5\. 別タブで Snyk の設定画面に自動で遷移します。**[Monitoring behavior on build]** を Never monitor に設定します。

<img src="/static/images/module7/01-05-managed-snyk-action.png" width=100%>

[設定値の説明](https://docs.snyk.io/integrations/ci-cd-integrations/aws-codepipeline-integration/setup-steps-for-aws-codepipeline#step-4-configure-settings)

6\. **[Continue]** をクリックします。

<img src="/static/images/module7/01-06-managed-snyk-action.png" width=100%>

7\. **[確認]** をクリックし、 OAuth リクエストを完了します。

<img src="/static/images/module7/01-07-managed-snyk-action.png" width=100%>

8\. リクエストが完了すると、 **プロバイダに正常にアクションを設定しました。** とアクション画面に表示されます。 **[完了]** をクリックして、アクションを設定しましょう。

<img src="/static/images/module7/01-08-managed-snyk-action.png" width=100%>

9\. さらにステージ編集の画面の **[完了]** をクリックし、パイプラインの **[保存する]** をクリックします。

<img src="/static/images/module7/01-09-managed-snyk-action.png" width=100%>

10\. 確認画面が表示されます。**[保存する]** をクリックします。

<img src="/static/images/module7/01-10-managed-snyk-action.png" width=100%>

11\. パイプラインの編集が完了すると **パイプラインが正常に保存されました。** と表示されるはずです。

<img src="/static/images/module7/01-11-managed-snyk-action.png" width=100%>

12\. SCA で検知させるために、 **requirements.txt** を元に戻してみます。 Cloud9 コンソールから、**flask-app** フォルダの下にある **requirements.txt** ファイルを開きます。

13\. **requirements.txt** を以下のように編集します。

```txt
click==8.1.3
Flask==2.2.3
Flask-SQLAlchemy==3.0.3
Flask-WTF==1.1.1
greenlet==2.0.2
importlib-metadata==6.0.0
itsdangerous==2.1.2
Jinja2==3.1.2
MarkupSafe==2.1.2
SQLAlchemy==2.0.5.post1
typing_extensions==4.5.0
Werkzeug==2.2.2
WTForms==3.0.1
zipp==3.15.0
wdb==3.3.0
setuptools==57.4.0
```

14\. CodeCommit に変更結果を以下のコマンドでプッシュします。

```bash
cd ~/environment/flask-app
git add .
git commit -a -m "Test SCA Tool"
git push
```

15\. パイプラインの実行が完了しました。 **[Snyk で表示]** をクリックして、検出結果を確認してみましょう。

<img src="/static/images/module7/01-12-managed-snyk-action.png" width=100%>

16\. Snyk で表示 をクリックすると、 HTML ベースのレポートが表示されます。 レポートは14日間保存されます。その後、パイプラインを実行すると、レポートが更新され、保存期間がリセットされます。

<img src="/static/images/module7/01-13-managed-snyk-action.png" width=100%>

17\. 時間があれば **requirements.txt** を修正、コミットして合格した時の挙動を確認してみましょう。

```txt
click==8.1.3
Flask==2.2.5
Flask-SQLAlchemy==3.0.3
Flask-WTF==1.1.1
greenlet==2.0.2
importlib-metadata==6.0.0
itsdangerous==2.1.2
Jinja2==3.1.2
MarkupSafe==2.1.2
SQLAlchemy==2.0.5.post1
typing_extensions==4.5.0
Werkzeug==2.2.3
WTForms==3.0.1
zipp==3.15.0
wdb==3.3.0
setuptools==65.5.1
```

```bash
cd ~/environment/flask-app
git add .
git commit -a -m "Fix Insecure Packages"
git push
```

マネージド Snyk アクションの組み込みを設定することができました。ハンズオンで利用したリソースの片付けを行います。

[Next: 片付け](../module8/crean-up.md)