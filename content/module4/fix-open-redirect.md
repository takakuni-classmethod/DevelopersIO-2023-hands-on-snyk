# オープンリダイレクト攻撃の修正

最後に **Open Redirect** と検知された部分を修正していきます。

<img src="/static/images/module4/06-01-fix-open-redirect.png" width=100%>

オープンリダイレクト攻撃は、ウェブアプリケーションがユーザーを不正で信頼できないサイトにリダイレクトさせることで発生します。一般的に、 URL リダイレクトとは、ウェブサイトやアプリケーションがユーザーを別のサイトにリダイレクトする機能のことを指します。これは、多くの場合、良心的で有用な機能です。

例えば、リソースが新しい場所に移動した場合、 URL リダイレクトはエラーメッセージを表示する代わりに、ユーザーをその場所に移動させることができます。しかし、この機能はソーシャルエンジニアリングによって悪用され、あるサイトにアクセスしているとユーザーを騙して、実際にはフィッシングサイトなどの危険なサイトにリダイレクトされることがあります。

1\. オープンリダイレクト攻撃を防ぐために、 **url_for** を利用して URL 直書きを修正します。 **a5.py** のコードを次のように置き換えます。

```python
from flask import (
    Blueprint,
    request,
    url_for,
    redirect,
    make_response,
    render_template
)

from models import (
    get_user,
    get_user_by_password
)

from utils import (
    generate_session,
    parse_session
)

bp = Blueprint(
    "a5", __name__,
    template_folder='templates',
    static_folder='static'
)

@bp.route("/A5")
def a5():
    return render_template("a5.html")

@bp.route("/A5/auth", methods=['POST'])
def a5_auth():
    username = request.form.get("username")
    password = request.form.get("password")
    user = get_user_by_password(username, password)
    if not user:
        return render_template("error.html", message="Invalid Credentials")
    
    # Generate SessionID
    session_id = generate_session(username)
    response = make_response(redirect(url_for("a5.a5_profile", username=username)))
    # deepcode ignore WebCookieMissesCallToSetSecure: This is test environment.
    response.set_cookie("sessionId", session_id, httponly=True)
    return response

@bp.route("/A5/profile/<username>")
def a5_profile(username):
    if not request.cookies.get("sessionId"):
        return ("<h1>Not Authorized!</h1>")
    session = parse_session(request.cookies.get("sessionId"))
    user = get_user(username)
    if not user:
        return render_template("404.html")
    return render_template("profile.html", user=user)
```

2\. 変更をローカルリポジトリにコミットしておきましょう。

```bash
cd ~/environment/flask-app
git commit -a -m "Fix SAST Findings"
```

[Next: ソフトウェア構成解析 (SCA)](../module5/index.md)