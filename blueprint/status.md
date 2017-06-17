# Group status

## 自身のステータスエンドポイント [/status]

### 自分自身のステータス更新 [PUT]

+ Request (application/json)
    + Headers
        Authorization : Bearer valid_access_token
    + Attributes
        + inBusiness: true (boolean) - 出社/退社(trueなら出社)
        + comment: 宝町 (string) - コメント
        + contact: 090ーXXXXーXXXX (string) - 連絡先

+ Response 200 (application/json)
    + Attributes
        + inBusiness: true (boolean) - 出社/退社(trueなら出社)
        + comment: 宝町 (string) - コメント
        + contact: 090ーXXXXーXXXX (string) - 連絡先
        
+ Response 401 (application/json)
    + Attributes
        + message: invalid token (string) - トークンの認証に失敗


+ Response 400 (application/json)
    + Attributes
        + message: user post is faild (string) - 送信パラメータの不正


### 自分自身のステータス取得 [GET]

+ Request
    + Headers
        Authorization : Bearer valid_access_token

+ Response 200 (application/json)
    + Attributes
        + inBusiness: true (boolean) - 出社/退社(trueなら出社)
        + comment: 宝町 (string) - コメント
        + contact: 090ーXXXXーXXXX (string) - 連絡先

        
+ Response 401 (application/json)
    + Attributes
        + message: invalid token (string) - トークンの認証に失敗


## 全員のステータスエンドポイント [/status/all]

### 全員のステータスを取得 [GET]

+ Request
    + Headers
        Authorization : Bearer valid_access_token

+ Response 200 (application/json)
    + Body
        [
            {userid: "userid123", comment:"宝町", contact: "090ーXXXXーXXXX",inBusiness: true, lastUpdate: "2017-03-31 15:30:31", name:"田中　太郎" },
            {userid: "userid456", comment:"YBP", contact: "080ーXXXXーXXXX",inBusiness: false, lastUpdate: "2017-03-31 15:30:31", name:"吉田　花子" }
        ]

+ Response 400 (application/json)
    + Attributes
        + message: no status (string) - ステータス情報が登録されていない

+ Response 401 (application/json)
    + Attributes
        + message: no Authorization (string) - トークンが送信されていない


+ Response 401 (application/json)
    + Attributes
        + message: invalid token (string) - トークンの認証に失敗

