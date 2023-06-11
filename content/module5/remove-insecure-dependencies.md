# 安全でない依存関係の修正

安全でない依存関係を修正するには、パッケージを置き換えるか、安全なバージョンにアップグレードまたはダウングレードする（必要がない場合は完全に削除する）ことが考えられます。

今回のケースでは、 **flask**, **werkzeug**, **setuptools** の古くて安全でないバージョンを使用していることが判明し、セキュリティ修正を行うためにバージョンを更新するように求められています。

1\. AWS Cloud9 に移動し、**flask-app** フォルダの下にある **requirements.txt** ファイルを開きます。

<img src="/static/images/module5/03-01-remove-insecure-dependencies.png">

2\. **flask** を **2.2.3** から **2.2.5**, **werkzeug** を **2.2.2** から **2.2.3**, **setuptools** を **57.4.0** から **65.5.1** にアップグレードしておきます。 **requirements.txt** ファイルを保存します。新しいバージョンの **requirements.txt** は、次のようになります。

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

3\. Cloud9 のターミナルウィンドウに移動し、以下のコマンドを入力して変更をコミット、プッシュします。

```bash
cd ~/environment/flask-app
git add .
git commit -a -m "Fix Insecure Packages"
git push
```

4\. プッシュが完了してしばらくすると、 **ApplicationSecurityChecks** が合格していることがわかります。また、 **BuildImage** に進み、 Docker イメージのビルドが進む仕組みとなっています。

<img src="/static/images/module5/03-02-remove-insecure-dependencies.png" width=100%>

5\. **BuildImage** ステージが終了すると、 Amazon ECR に新しいコンテナイメージが公開されているのが確認できるかと思います。このイメージを使って、次のセクションで Amazon ECS で実行されている現在の **flask-app** タスクを置き換えます。

<img src="/static/images/module5/03-03-remove-insecure-dependencies.png" width=100%>

[Next: 安全なコードレビュー](../module6/index.md)