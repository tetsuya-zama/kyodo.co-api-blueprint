# Group user

## ユーザーエンドポイント [/user]

### 新規ユーザー作成 [POST]

+ Request (application/json)
    + Attributes
        + userid: test_user_id (string, required) - 登録するユーザーID
        + name: テストユーザー (string) - 登録する名前
        + password: test_user_pass (string) - 登録するパスワード

+ Response 200 (application/json)
    + Attributes
        + token: valid_access_token (string) - アクセストークン
        + name: テストユーザー (string) - ユーザー名

+ Response 400 (application/json)
    + Attributes
        + message: user post is faild (string) - 登録処理に失敗（ユーザ名の重複など）

### パスワード/名前の変更 [PUT]

+ Request (application/json)
    + Headers
        Authorization : Bearer valid_access_token
    + Attributes
        + newPassword: test_user_new_pass (string) - 新しいパスワード
        + name: 新テストユーザー (string) - 新しい名前

+ Response 200 (application/json)
    + Attributes
        + newPassword: test_user_new_pass (string) - 新しいパスワード
        + name: 新テストユーザー (string) - 新しい名前

+ Response 401 (application/json)
    + Attributes
        + message: invalid token (string) - トークンの認証に失敗

        

### ユーザー削除(未実装) [DELETE]

+ Request (application/json)
    + Headers
        Authorization : Bearer valid_access_token
    + Attributes
        + userid: correct_userid (string) - ユーザーID
        + password: correct_password (string) - パスワード

+ Response 200

### ログインユーザーの名前参照 [GET]

+ Request
    + Headers
        Authorization : Bearer valid_access_token

+ Response 200 (application/json)
    + Attributes
        + name: テストユーザー (string) - ログインユーザーの名前

+ Response 401 (application/json)
    + Attributes
        + message: invalid token (string) - トークンの認証に失敗
