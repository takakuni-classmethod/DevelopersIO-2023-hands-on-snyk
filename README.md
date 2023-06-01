# Security for Developers
## 開発者のためのセキュリティとは?

セキュリティは全員の責任です。アプリケーションに適切な構成を早期に組み込むことができれば、安全かつ迅速に提供するという目標を達成しやすくなります。このワークショップで学ぶテクニックは、構築するアプリケーションのセキュリティレベルを上げるのに役立つでしょう。これにより、顧客に価値を提供するソフトウェアの構築により多くの時間を費やし、セキュリティレビュー後のやり直しにかかる時間を減らすことができます。

このワークショップでは、自分が構築したアプリケーションのセキュリティについて考える方法を学びます。一般的なセキュリティリスクと、ソフトウェアデリバリーに大きな影響を与えることなくアプリケーションを保護するために使用できるツールとテクニックについて説明します。

### 概要

このワークショップでは、開発者はネイティブな AWS の開発者向けツールを使用して自動リリースパイプラインをセットアップし、安全でないウェブアプリケーションをデプロイします。その過程で一般的なセキュリティリスクを調査し、それらがどのように悪用されているかを説明します。次に、いくつかのセキュリティツール/プロセスを導入し、リリースパイプラインに統合して、コード変更ごとに実行されるようにします。また、これらの自動および手動のプロセスを通じて特定されたすべてのセキュリティリスクを是正します。

このワークショップが終わるまでに、以下のようなアプリケーションセキュリティステージを持つリリースパイプラインが構築されます。

<img src="/static/images/全体構成図.png" alt="全体構成図" width="100%">

最終目標は、安全でないウェブアプリケーションを修正し、より安全な状態でリリースすることです。

### 所要時間

このワークショップには n 時間かかります。省略できるオプションモジュールもありますが、時間をかけてすべて試してみることを強くお勧めします。

### 構成

- モジュール 1 - はじめに
- モジュール 2 - リリースの自動化
- モジュール 3 - OWASP Top 10
- モジュール 4 - 静的アプリケーションセキュリティテスト (SAST)
- モジュール 5 - ソフトウェア構成解析 (SCA)
- モジュール 6 - セキュアコードレビュー (残りの脆弱性の修正)

### 事前知識

正常なラボの完了にあたって、AWS のインフラなどの基本的なサービス、Python プログラミング言語、Git、およびコマンドライン (bash) に関する基礎知識を持っていることを推奨します。なお、Web アプリケーションは Python で書かれていますが、すべての概念とツールはあらゆるプログラミング言語とフレームワークにも応用できます。

[Next](./content/module1/開発環境のセットアップ.md)