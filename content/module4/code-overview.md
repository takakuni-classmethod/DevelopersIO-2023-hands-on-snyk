# コードの概要

コードを修正するに、 Web アプリケーションのコードベースがどのように構成されているのか、簡単に説明します。

```
   - flask-app
     - app.py
     - models.py
     - utils.py
     - pages/
         - a1.py
         - a2.py
         - a3.py
         - a5.py
         - a6.py
         - a7.py
         - a9.py
     - templates/
         - a1.html
         - a2.html
         - a3.html
         - a5.html
         - a6.html
         - a7.html
         - a9.html
     - static/
```

- **app.py** - Web アプリケーションは Flask フレームワークを使用して実装されています。 **app.py** は Web アプリケーションのメインエントリーポイントで、すべてのページをプロビジョニングし、データベースをブートストラップします。
- **models.py** - Object Relational Mapper のライブラリである SQLALchemy で定義されたデータベースモデルを含んでいます。また、オブジェクトをクエリするためのヘルパー関数も含まれています。このワークショップでは、簡単に説明するために、 Web アプリケーションはデータベースとして SQLite を使用します。
- **utils.py** - ページが共有するヘルパー関数のセットです。セッションクッキーはここで生成されます。
- **pages/*.py** - pages フォルダは、Web アプリケーションの各ページの実装を含んでいます。後でデバッグやナビゲーションを容易にするために、OWASP Top 10 の脆弱性を示す各ページは、それ自身の python ファイルに収容されます (例: A1: Injection は pages/a1.py に書かれます、など)。
- **templates/*.html** - Jinja2 で書かれた HTML テンプレートが含まれており、Web ページをレンダリングするために使用されます。ページと同様に、各テンプレートは、それ自身の HTML ファイル内の OWASP Top 10 の脆弱性にちなんで命名されます（例：A1: Injection は templates/a1.html に書かれています、など）。
- **static** - Web アプリケーションで使用される静的コンテンツが含まれます。

AWS Cloud9 で各ファイルを開いて確認することができます。次のセクションで、 Snyk Code で検出されたコードの修正を進めていきます。

[Next: クッキーの保護](./protect-cookies.md)