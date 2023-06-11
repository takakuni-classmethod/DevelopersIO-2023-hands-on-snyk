# セキュアなトークンの生成

**flask-app** 配下の **utils.py** を開くと、以下のようなコードになっています。

```python
import json
import base64
from datetime import datetime, timezone

def generate_session(username):
    ### Generate sessionId
    session_obj = {"username": username, "timestamp": datetime.now(timezone.utc).isoformat()}
    session_id = base64.b64encode(json.dumps(session_obj).encode("utf-8"))
    return session_id

def parse_session(session_obj):
    ### Parse sessionId
    session_obj = json.loads(base64.b64decode(session_obj).decode("utf-8"))
    return session_obj
```

**sessionId** は **generate_session** 関数で生成されています。セッション ID は、ユーザー名とタイムスタンプのフィールドを含む **base64** エンコードされた JSON オブジェクトであるため、非常に予測しやすい方法で生成されます。 **[Salt](https://en.wikipedia.org/wiki/Salt_(cryptography))** を追加するだけで、 Broken Authentication を防止することができます。手っ取り早く解決するために、 **[secrets](https://docs.python.org/3/library/secrets.html#module-secrets)** を使ってセッションオブジェクトにランダムな値を入れてみましょう。 secrets モジュールは、パスワードやセキュリティトークンの管理に適した暗号化された強力な乱数を提供します。

1\. **utils.py** の中身を以下のコードに置き換えてみてください。

```python
import secrets
import json
import base64
from datetime import datetime, timezone

def generate_session(username):
    ### Generate sessionID
    session_obj = {"username": username, "timestamp": datetime.now(timezone.utc).isoformat(), "salt": secrets.token_urlsafe()}
    session_id = base64.b64encode(json.dumps(session_obj).encode("utf-8"))
    return session_id

def parse_session(session_obj):
    ### Parse sessionId
    session_obj = json.loads(base64.b64decode(session_obj).decode("utf-8"))
    return session_obj
```

他のプログラミング言語のセキュア乱数ジェネレーターついては、[こちら](https://cheatsheetseries.owasp.org/cheatsheets/Cryptographic_Storage_Cheat_Sheet.html#secure-random-number-generation)で確認できます。

> **Warning**
> これによって sessionId が予測しにくくなるはずです。しかし、認証されたユーザー（メモリやデータベースに保存されたトークンが発行された場合）のリクエストごとに Salt を検証する必要があるため、 **完全に Broken Authentication の問題を完全に解決するものではありません。** 完全な解決のためには、自分で実装するか [Flask-Login](https://flask-login.readthedocs.io/en/latest/) の使用、または [Amazon Cognito](https://aws.amazon.com/cognito/) などのアイデンティティサービスを使用する方法があります。

> token_urlsafe 関数は、ランダムで URL セーフなテキスト文字列を生成します。デフォルトでは、32 バイト 相当のランダムな文字列が生成されます。少なくとも 2015 年時点では、現在の計算能力から保護するには 32バイトで十分であると考えられていました 。文字列のサイズは自分で指定することも、デフォルトのままにしておくこともできます（時間の経過とともに要件は変化します）

その他の脆弱性については、以下の URL から修正できます。

[Security for Developers - 8. セキュアコードレビュー](https://catalog.workshops.aws/sec4devs/ja-JP/module8/enable-csrf-protection)

```
cd ~/environment/flask-app
git add .
git commit -m 'Fix Broken Authentication'
git push
```

[Next: ECS タスクの更新](update-ecs-task.md)