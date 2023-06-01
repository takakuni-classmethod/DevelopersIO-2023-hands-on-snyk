# 開発環境のセットアップ
## AWS Cloud9 をセットアップする

このワークショップには [AWS Cloud9](https://aws.amazon.com/jp/cloud9/) が開発環境として最適です。このワークショップに必要なすべてのソフトウェアがすでにプリインストールされているため、作業中のトピックに集中する時間が節約されます。

1\. AWS コンソールの検索バーに **Cloud9** と入力し、**[ 環境を作成 ]** をクリックします。

<img src="./../../static/images/module1/01_create_environment.png" width="100%">

2\. 環境の名前と説明（例えば 名前 に devio2023-snyk-workshop など。Description は任意です。）を入力します。

3\. 環境タイプは **新しい EC2 インスタンス** を選択します。

<img src="./../../static/images/module1/02_create_environment.png" width="100%">

4\. インスタンスタイプは **t2.micro (1 GiB GiB RAM + 1 vCPU)** 、プラットフォームは **Amazon Linux 2** 、タイムアウトは **30 分** を選択します。

<img src="./../../static/images/module1/03_create_environment.png" width="100%">

5\. ネットワーク設定で Cloud9 環境への接続方法、 VPC とサブネットの選択を行います。接続方法は **AWS Systems Manager (SSM)** を、 サブネットは **SSM エンドポイントへ到達可能なサブネット** を選択してください。

<img src="./../../static/images/module1/04_create_environment.png" width="100%">

6\. タグは付与せず **[ 作成 ]** をクリックします。

<img src="./../../static/images/module1/05_create_environment.png" width="100%">

7\. 数分後、Cloud9 にログインができ、ワークショップの準備が整うはずです。

<img src="./../../static/images/module1/06_create_environment.png" width="100%">

[Next](../module2/README.md)