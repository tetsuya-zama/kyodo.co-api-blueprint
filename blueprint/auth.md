# Group auth

## 認証エンドポイント [/auth]

### IDとパスワードによる認証を行う [POST]

+ Request 正しいID/Pass (application/json)
    + Attributes
        + userid: correct_userid (string) - ユーザーID
        + password: correct_password (string) - パスワード

+ Response 200 (application/json)
    + Attributes
        + token: valid_access_token (string) - アクセストークン
        + name: テストユーザー (string) - ユーザー名

+ Request 不正なID/Pass (application/json)
+ Attributes
    + userid: invalid_userid (string) - ユーザーID
    + password: invalid_password (string) - パスワード

+ Response 204
