# Snyk で作るコンテナイメージパイプライン

このワークショップは AWS から提供されている [Security for Developers](https://catalog.workshops.aws/sec4devs/en-US) ワークショップの一部を Snyk に置き換え、 Snyk を体験いただくワークショップです。

## 事前準備

このワークショップでは、以下のアカウントが必要です。

- AWS アカウント
- 以下のいずれかのアカウント（Snyk へのアカウント登録に利用します)
  - Gmail
  - GitHub
  - BitBucket
  - AzureAD
  - Docker ID

## 前提知識
### SCA とは

SCA (Software Composition Analysis) とは、ソースコードで利用されている、オープンソースのセキュリティ解析を指します。

Snyk Open Source は SCA 製品の 1 つで、各オープンソースの依存関係を含めて、オープンソースの脆弱性を解析します。

### SAST とは

SAST (Static Application Security Testing) とは、ソースコードに対してのセキュリティ解析を指します。

Snyk Code は SAST 製品の 1 つで、オープンソースコミットを学習エンジンとした AI を利用し、誤検知が少なくなるよう日々開発されている製品です。

## 構成

今回は以下の構成になります。
このワークショップでは、 Snyk Open Source と Snyk Code を利用します。

APPENDIX として、AWS CodePipeline と Snyk Open Source の統合機能のハンズオンもありますので、時間が余ったら試してみてください。

<img src="/static/images/diagrams.png" width="100%">

[Next：開発環境のセットアップ](./content/module1/aws-cloud9.md)