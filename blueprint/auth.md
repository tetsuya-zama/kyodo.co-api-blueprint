# Group auth

## 認証エンドポイント [/auth]

### IDとパスワードによる認証を行う [POST]

+ Request (application/json)
事前にシステム登録されているユーザIDとパスワードを送信する
    + Attributes
        + userid: correct_userid (string, required) - ユーザーID
        + password: correct_password (string, required) - パスワード

+ Response 200 (application/json)
ユーザIDとパスワードにより認証された。tokenは認証の都度再発行される。nameはユーザ登録時に利用者が決定したものでkey情報ではない
    + Attributes
        + token: valid_access_token (string) - アクセストークン
        + name: テストユーザー (string) - ユーザー名

+ Request 不正なID/Pass (application/json)
+ Attributes
    + userid: invalid_userid (string) - ユーザーID
    + password: invalid_password (string) - パスワード

+ Response 204



### ログアウト [DELETE]
+ Request 認証済みトークン (application/json)
    + Headers
        Authorization : Bearer valid_access_token

+ Response 200 (application/json)
    + Attributes
        + message: ok (string) - ログアウト完了：Token無効化

+ Response 401 (application/json)
    + Attributes
        + message: invalid token (string) - トークンの認証に失敗