# Group user

## ユーザーエンドポイント [/user]

### 新規ユーザー作成 [POST]

+ Request (application/json)
    + Attributes
        + userid: test_user_id (string, required) - 登録するユーザーID
        + name: テストユーザー (string) - 登録する名前
        + password: test_user_pass (string) - 登録するパスワード
        + secretQuestion: 母親の旧姓は？ (string, optional ) - 登録する秘密の質問
        + secretAnswer: 佐藤 (string, optional) - 秘密の質問の答え
        + contact: 0300000000 (string, optional) - デフォルト連絡先

+ Response 200 (application/json)
    + Attributes
        + token: valid_access_token (string) - アクセストークン
        + name: テストユーザー (string) - ユーザー名

+ Response 400 (application/json)
    + Attributes
        + message: user post is faild (string) - 登録処理に失敗（ユーザ名の重複など）

### パスワード/名前の変更 [PUT]
このサービスはいずれ移行予定

+ Request (application/json)
    + Headers
        Authorization : Bearer valid_access_token
    + Attributes
        + newPassword: test_user_new_pass (string) - 新しいパスワード
        + name: 新テストユーザー (string) - 新しい名前
        + contact: 0300000000 (string,optional) - デフォルト連絡先

+ Response 200 (application/json)
    + Attributes
        + newPassword: test_user_new_pass (string) - 新しいパスワード
        + name: 新テストユーザー (string) - 新しい名前
        + contact: 0300000000 (string) - デフォルト連絡先

+ Response 401 (application/json)
    + Attributes
        + message: invalid token (string) - トークンの認証に失敗

        

### ユーザー削除 [DELETE]
このサービスはいずれ移行予定

+ Request (application/json)
    + Headers
        Authorization : Bearer valid_access_token

+ Response 200 (application/json)
    + Attributes
        + message: ok (string) - ユーザ削除完了

### ログインユーザーの名前参照 [GET]
このサービスはいずれ移行予定

+ Request
    + Headers
        Authorization : Bearer valid_access_token

+ Response 200 (application/json)
    + Attributes
        + name: テストユーザー (string) - ログインユーザーの名前
        + contact: 033333333 (string) - デフォルト連絡先

+ Response 401 (application/json)
    + Attributes
        + message: invalid token (string) - トークンの認証に失敗



## ユーザに関する操作エンドポイント [/user/{userId}]

+ Parameters
    + userId: taro1234 (string) - 操作したいユーザID

### ユーザ設定情報の取得 [GET]
ユーザのプロファイルを取得する。

+ Request
    + Headers
        Authorization : Bearer valid_access_token

+ Response 200 (application/json)
    + Attributes
        + name: テストユーザー (string) - ログインユーザーの名前
        + contact: 0300000000 (string) - デフォルト連絡先

+ Response 401 (application/json)
    + Attributes
        + message: invalid token (string) - トークンの認証に失敗




## ユーザ毎履歴取得エンドポイント [/user/{userId}/history]

+ Parameters
    + userId: taro1234 (string) - 操作したいユーザID


### ユーザー履歴取得 [GET]
ユーザ登録履歴を取得する。

+ Request (application/json)
    + Headers
        Authorization : Bearer valid_access_token

+ Response 200 (application/json)
    + Body
        [
            {"userid": "taro1234", 
             "datetime" : 2017-07-12 22:55:01.623286,
             "comment" : "123会議室に居ます",
             "contact" : "0333333333",
             "inBusiness" : true
            },
            {"userid": "taro1234", 
             "datetime" : 2017-07-12 22:55:01.623286,
             "comment" : "234会議室に居ます",
             "contact" : "0333333333",
             "inBusiness" : true
            }
        ]


+ Response 204 (application/json)
    + Attributes
        + message: no history (string) - 履歴無し

+ Response 404 (application/json)
    + Attributes
        + message: no useruser  (string) - そんなユーザはいないです


## 秘密の質問エンドポイント [/user/{userId}/secretquestion]

+ Parameters
    + userId: taro1234 (string) - 操作したいユーザID


### 秘密の質問取得 [GET]
ユーザ登録時に設定した、秘密の質問を取得する。

+ Request (application/json)

+ Response 200 (application/json)
    + Attributes
        + secretQuestion: "母親の旧姓は？" (string) - 設定している秘密の質問

+ Response 204 (application/json)
    + Attributes
        + message: no secretQuestion (string) - 設定している秘密がない

+ Response 404 (application/json)
    + Attributes
        + message: no useruser  (string) - そんなユーザはいないです


### 秘密の質問答え合わせ [POST]
秘密の質問に対する答えがあっているか判定

+ Request (application/json)
    + Attributes
        + secretAnswer: 佐藤 (string, optional) - 秘密の質問の答え
        + password: test_user_pass (string) - 新規に登録するパスワード

+ Response 200 (application/json)
    + Attributes
        + message : ok (string) - 秘密の質問の答えがあったので、パスワードを再設定完了

+ Response 400 (application/json)
    + Attributes
        + message: not match (string) - 秘密の質問が不一致